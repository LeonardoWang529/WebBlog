---
title: Web 开发经验和教训
date: 2017-12-06 08:19:23
tags:
- web
categories: 'Web Front'
---

View: Layout -> JS: Controller -> JS:server -> php: RestServer -> php: include function
以下是实现 整套restful function的从最前到最后的操作流程

1. 在前端用 html tag 做 input；
   用angularJs 去到uploaded file 并且call

{% codeblock lang:html %}
<a  data-ng-click="browseFile('.upfile')">upload</a>
<input type="file" name="file" class="upfile" id="upfile" onchange="angular.element(this).scope().uploadFile(this.files)" style="display: none;"/>
{% endcodeblock %}

这里的 data-ng-click="browseFile('.upfile') call 的是 js file 里面的 $scope.browseFile = function (fileInputClass)
在input 里面 onchange call 到的是 $scope.uploadFile = function (files) ； 这个files将会是一个jason object， 可以通过 files[0]['type'] 来 取得它的情况

2. 在js曾实现browseFile 和 uploadFile

{% codeblock lang:js %}
angular.module('lungflute').controller('LoginController', function ( $scope, $rootScope, loginService, $timeout, $location, $translate, $sessionStorage, $http, commonFunction, patientService,socket) {
	$scope.browseFile = function (fileInputClass) {
        	var $elm=$(fileInputClass);
        	var $clone=$elm.clone();
        	$clone.val("");
        	$elm.replaceWith($clone);
        	$timeout(function() {
            	angular.element(fileInputClass).trigger('click');
        	}, 100);
    	};

	$scope.uploadFile = function (files) {
		fd.append("file", files[0]);
   		patientService.sendChatFile2(fd).success(function (data) {}).error(function () {});
	};
}
{% endcodeblock %}

这里 在 angularjs的controller 里 加入了 patientService 所以可以直接用 里面的function。

3. 在js 的 server 层实现

{% codeblock lang:js %}
app.factory('patientService', function($http, $sessionStorage, $rootScope,commonFunction,serviceUtil) {
	bluejayAPI.sendChatFile2 = function(fd) {
        return $http({
            method: 'POST',
            url: window.location.protocol + '//' + document.domain +'/PT2/httpdocs/v4_5/' + 'UploadFileInChat2',
            data: fd,
            withCredentials: false,
            headers: {'Content-Type': undefined },
            transformRequest: angular.identity,
            responseText: 'JSON'
        });
    }
}
{% endcodeblock %}

通过这里的rest call 把 file post到 后端的 一个叫 UploadFileInChat2 的 function 接口。

4. 在 php 层面 把 所有的 RestServer function （在php include下面的 function）全部 mapping 成 string， 在找到与传来的function name相同的 string 与 function 进行执行。

{% codeblock lang:php %}
<?php
        $server = new RestServer($mode);
        $patterns = array();
        $patterns[0] = '/' . $version . '\/includes\//';
        $patterns[1] = '/.php/';
        $replacements = array();
        $replacements[0] = '';
        $replacements[1] = '';

        foreach (glob($version ."/includes/*.php") as $filename)
        {
                if (strstr($filename, "Rest.php"))
                {
                        include_once( $filename );
                        $classname = preg_replace($patterns, $replacements, $filename);
                        $server->addClass($classname);
                }
        }
	$_SERVER['REQUEST_URI']  = str_replace('/' . $version, '', $requestUri);
?>
{% endcodeblock %}

在这个层面里，有security 层级。 要么用 token 等通过security，要么把 这个 restcall 加入到 能绕过 security的list中。

5. 使用 include 下面的不同 php 文件内的 function 执行 php 操作 或与 DB互动

{% codeblock lang:php %}
<?php
class LFWebExtraFunctionRest {

    /**
     * @url POST /UploadFileInChat2
     */
    public function PostSendChatFile2($data) {
        $tmp_name = $_FILES["file"]["tmp_name"];
        $name = $_FILES["file"]["name"];
	$videoPathToUpload = '/var/www/release/efs/test.mp4';
	echoo (rename($tmp_name, $videoPathToUpload));
	exit;
    }
}
?>
{% endcodeblock %}

在这个特定的例子里，传入的值是一个 FILES 所以可以用 $_FILES 去取值
这里我们执行的操作是简单的移动到另一个文件夹下。
