# ajaxSearch
ajax+jsonp跨域搜索的实现
### @author林剑敏
### 静态内容的实现
### 有一个居中背景图，图里嵌套一个logo加表单form
```html
<body>
  <div class="bg-div">
    <div class="search-box">
      <div class ="logo"></div>
      <form id="search-form" action="https://cn.bing.com/search" target="_blank" id="search-form">
        <input type="text" class="search-input-text" id="search-input" autocomplete="off" name="q">
        <input type="submit" class="search-input-button" value="" id="search-submit">
      </form>
    </div>
  </div>
  <div class="suggest" id="search-suggest" style="display:none">
    <ul id="search-result">
      <li>搜索结果1</li>
      <li>搜索结果2</li>
    </ul>
  </div>
</body>
```

### 样式实现
```css
body {
    background-color: #333;
  }
  .bg-div {
    background-image: url(river.jpg);
    width: 1228px;
    height: 690px;
    margin: 0 auto;
    position: relative;
  }
  .logo {
    margin: -4px 18px 0 0;
    background-image: url(logo.png);
    width: 107px;
    height: 53px;
    float: left;
  }
  form {
    float: left;
    background-color: #fff;
    padding: 5px;
  }
  .search-input-text {
    border: 0;
    float: left;
    height: 25px;
    line-height: 25px;
    outline: none;
    width: 350px;
  }
  .search-input-button {
    border: 0;
    background-image: url(search-button.png);
    width: 29px;
    height: 29px;
    float: left;
    cursor: pointer;
  }
  .search-box {
    position: absolute;
    top: 200px;
    left: 300px;
  }
  .suggest {
    width: 388px;
    background-color: #fff;
    border: 1px solid #999;
  }
  .suggest ul {
    list-style: none;
    margin: 0;
    padding: 0;
  }
  .suggest ul li {
    padding: 3px;
    font-size: 14px;
    line-height: 25px;
    cursor: pointer;
  }
  .suggest ul li:hover {
    text-decoration: underline;
    background-color: #e5e5e5;
  }
```

### ajax部分解析
```javascript
$.ajax({
           type: "get",//请求方式
           async: false,//默认为true，默认情况为异步请求，同步请求改为false，我们这里暂且改为flase，让用户在请求完成后再进行下一步操作
           url: "http://api.bing.com/qsonhs.aspx?type=cb&cb=callback&q=" + inputText,//发送请求的地址
           dataType: "jsonp",//预期浏览器返回的数据类型
           jsonp: "callback",//在一个 jsonp 请求中重写回调函数的名字
           jsonpCallback:"callback",//为 jsonp 请求指定一个回调函数名
           success: function (data) {//请求成功后的回调函数
               callback(data);
           },
           error: function (data) {//请求失败调用的函数
               console.log(data);
           }
       });
```
### 实现的效果
![image](https://github.com/say-hello-user/ajaxSearch/blob/master/image/main.png)
