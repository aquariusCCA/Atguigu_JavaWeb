# 什么是ajax

+ AJAX = Asynchronous JavaScript and XML（异步的 JavaScript 和 XML）。

+ AJAX 不是新的编程语言，而是一种使用现有标准的新方法。

+ AJAX 最大的优点是在不重新加载整个页面的情况下，可以与服务器交换数据并更新部分网页内容。

+ AJAX 不需要任何浏览器插件，但需要用户允许 JavaScript 在浏览器上执行。

+ XMLHttpRequest 只是实现 Ajax 的一种方式。

**ajax工作原理：**

![](images/image_bjXPJoLb6a-1690508517199.png)

+ 简单来说，我们之前发的请求通过类似 form 表单标签、a 标签这种方式，现在通过运行 js 代码动态决定什么时候发送什么样的请求
+ 通过运行 JS 代码发送的请求浏览器可以不用跳转页面，我们可以在 JS 代码中决定是否要跳转页面
+ 通过运行 JS 代码发送的请求，接收到返回结果后，我们可以将结果通过 dom 编程渲染到页面的某些元素上，实现局部更新

# 如何实现 ajax 请求

> 原生 **javascript 方式进行 ajax(了解) :**

``` html
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Random User Generator Example</title>
</head>
<body>
<h1>Random User Generator Example</h1>

<div id="user-info"></div>

<button onclick="getUser()">Get Random User</button>
<button onclick="createUser()">Create Random User</button>

<script>
function getUser() {
  var xhr = new XMLHttpRequest();
  // 设置请求方式和请求的资源路径
  xhr.open("GET", "https://randomuser.me/api/", true);
  // 设置回调函数处理响应结果
  xhr.onreadystatechange = function () {
    if (xhr.readyState === 4 && xhr.status === 200) {
      var response = JSON.parse(xhr.responseText);
      displayUserInfo(response.results[0]);
    }
  };
  // 发送请求
  xhr.send();
}

function displayUserInfo(user) {
  var userInfo = document.getElementById("user-info");
  userInfo.innerHTML = `
    <img src="${user.picture.large}" alt="User Picture">
    <p>Name: ${user.name.first} ${user.name.last}</p>
    <p>Email: ${user.email}</p>
    <p>Location: ${user.location.city}, ${user.location.country}</p>
  `;
}

function createUser() {
  var xhr = new XMLHttpRequest();
  // 设置请求方式和请求的资源路径
  xhr.open("POST", "https://randomuser.me/api/", true);
  xhr.setRequestHeader("Content-Type", "application/json;charset=UTF-8");
  // 设置回调函数处理响应结果
  xhr.onreadystatechange = function () {
    if (xhr.readyState === 4 && xhr.status === 201) {
      var response = JSON.parse(xhr.responseText);
      displayUserInfo(response.results[0]);
    }
  };
  // 发送请求
  xhr.send();
}
</script>

</body>
</html>
```

**為甚麼 getUser() 方法中沒有 `xhr.setRequestHeader("Content-Type", "application/json;charset=UTF-8");` ?**

在 `getUser()` 方法中不需要設置 `Content-Type` 標頭，因為 GET 請求不包含主體，而是將資料附加在 URL 上。 `Content-Type` 標頭通常用於指定請求主體的類型，但在 GET 請求中通常不需要。

