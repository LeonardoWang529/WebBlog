---
title: AWS Simple Queue Service (SQS)
date: 2017-11-15 09:31:53
tags:
- AWS
- SQS
categories: "Web Server"
---

Amazon Simple Queue Service (SQS) is a fully managed message queuing service that makes it easy to decouple and scale microservices, distributed systems, and serverless applications.

SQS是一个非常便宜，容易维护使用的Queue。在做一些信息搬运的时候非常好用。

## 1. 项目：
Server PHP

## 2. 问题：
当大量用户使用把BroadCasting feature，而 BroadCasting 通道有只有一个的时候。
BroadCasting 将会 阻碍 instance的 正常工作。

## 3. 解决办法：
把BroadCasting 的 message 放到 SQS 里， 送到 另一个instance上去处理。

## 4. SQS 实现：


###  问题步骤
在使用 client -> ReceiveMessage(); 的时候会获得一个nested jason：
无法通过jason_decode直接把数据取出，原本Document内也没有说明。
解决方法如下:
      **使用$result->getPath('Message/0/date');**

Getting nested values
The getPath() method of the model is useful for easily getting nested values from a response. The path is specified as a series of keys separated by slashes.

```
// Perform a RunInstances operation and traverse into the results to get the InstanceId
$result = $ec2Client->runInstances(array(
    'ImageId'      => 'ami-548f13d',
    'MinCount'     => 1,
    'MaxCount'     => 1,
    'InstanceType' => 't1.micro',
));
$instanceId = $result->getPath('Instances/0/InstanceId');
```

Wildcards are also supported so that you can get extract an array of data. The following example is a modification of the preceding such that multiple InstanceIds can be retrieved.

```
// Perform a RunInstances operation and get an array of the InstanceIds that were created
$result = $ec2Client->runInstances(array(
    'ImageId'      => 'ami-548f13d',
    'MinCount'     => 3,
    'MaxCount'     => 5,
    'InstanceType' => 't1.micro',
));
$instanceId = $result->getPath('Instances/*/InstanceId');

```
More info: http://docs.aws.amazon.com/aws-sdk-php/v2/guide/feature-models.html
******
