---
title: ReactJs RemotePath setup
date: 2020-03-29 01:49:26
tags:
- server
categories: 'Web FrontEnd'
---

In a ReactJs Application, if we want to deploy to web server but not on the server structure root path. we will receive an error: can not find main.5ecd60fb.chunk.css ..
The reason is, the index of react component is looking for /static/css/main.5ecd60fb.chunk.css
However, the real path is /somename/static/css/main.5ecd60fb.chunk.css

To solve this issue, react give a setting in package.json file: "homepage": "."
With this, you can setup the landing position of your react component:
"homepage":"http://xxxxx.com/somename"
After this, the index will looking for folder and file under somename path.

Same problem will happen on page redirection:
{% codeblock %}
handleSubmit(e){
  e.preventDefault();
  window.location ='/page2';
}
{% endcodeblock %}
if we use window.location. It will go get the current page address (URL) and to redirect the browser to a new page. We know that the current path is "http:/xxxxx.com/somename/page1" if we use window.location it will redirect to "http:/xxxxx.com/page2" which is not correct.

To solve this, we use another redirect function
{% codeblock %}
handleSubmit(e){
  e.preventDefault();
  this.props.history.push("/page2")
}
{% endcodeblock %}

return <Redirect to='/dashboard' /> can also do the trick. However if this is been called in a function not render method. the Redirect will not work.

change process.env.PUBLIC_URL will also ok.

Resources Link: https://create-react-app.dev/docs/deployment/

Using Object store to localstorage. some browser may support different ways
