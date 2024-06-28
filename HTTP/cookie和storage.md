# 总结

简述cookie和localStorage以及sessionStorage的区别。
关于cookie、sessionStorage、localStorage三者的区别主要有以下几点：
存储大小：cookie数据大小不能超过4k，sessionStorage和localStorage虽然也有存储大小的限制，但比cookie大得多，可以达到5M或更大
有效时间：localStorage存储持久数据，浏览器关闭后数据不丢失除非主动删除数据；sessionStorage数据在当前浏览器窗口关闭后自动删除；cookie设置的cookie过期时间之前一直有效，即使窗口或浏览器关闭
数据与服务器之间的交互方式，cookie的数据会自动的传递到服务器，服务器端也可以写cookie到客户端；sessionStorage和localStorage不会自动把数据发给服务器，仅在本地保存

## cookie

    存储在客户端并随每个请求发送到服务器。
    最大容量一般为4KB。
    设置时可以指定过期时间、路径、域和安全标志。
    用于服务器和客户端之间的数据传递，比如用户会话管理、记住登录状态等。

  ``javascript
  // 设置cookie
document.cookie = "username=John; expires=Thu, 18 Dec 2023 12:00:00 UTC; path=/";

// 读取cookie
const cookies = document.cookie.split(';').reduce((cookies, cookie) => {
    const [name, value] = cookie.split('=').map(c => c.trim());
    cookies[name] = value;
    return cookies;
}, {});

// 删除cookie
document.cookie = "username=; expires=Thu, 01 Jan 1970 00:00:00 UTC; path=/";
``

## sessionStorage

存储在客户端，不随请求发送到服务器。
最大容量为5-10MB（不同浏览器可能略有不同）。
数据仅在浏览器会话期间有效，关闭标签页或浏览器后数据即被清除。
适合用于临时数据存储，如一次性表单数据、会话状态等。

``javascript
// 设置数据
sessionStorage.setItem('username', 'John');

// 获取数据
const username = sessionStorage.getItem('username');

// 删除数据
sessionStorage.removeItem('username');

// 清空所有数据
sessionStorage.clear();
``

## localStorage

存储在客户端，不随请求发送到服务器。
最大容量为5-10MB（不同浏览器可能略有不同）。
数据永久存储，除非手动删除。
适合用于存储较大的数据，如用户偏好设置、长时间不变的数据等。
``javascript
// 设置数据
localStorage.setItem('username', 'John');

// 获取数据
const username = localStorage.getItem('username');

// 删除数据
localStorage.removeItem('username');

// 清空所有数据
localStorage.clear();

``

## 结语

我之前回答问题 总是一句话说完了 真是太差劲了
Cookie：用于服务器和客户端之间的数据传递，常用于会话管理和保持用户状态。
localStorage：用于持久化存储客户端数据，适合存储较大的、长期不变的数据。
sessionStorage：用于临时存储客户端数据，适合在一个会话内临时保存数据。
