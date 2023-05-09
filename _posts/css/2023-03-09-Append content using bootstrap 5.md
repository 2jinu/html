---
title       : "Append content using bootstrap 5"
date        : 2023-03-09 16:19
categories  : [css]
tags        : [html, css, front end, bootstrap]
img_path    : /assets/img/posts/css
---

## Overview

<p class="codepen" data-height="300" data-theme-id="dark" data-default-tab="result" data-slug-hash="eYLepEe" data-user="ejinu" style="height: 300px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;">
  <span>See the Pen <a href="https://codepen.io/ejinu/pen/eYLepEe">
  Append content using bootstrap 5</a> by ejinu (<a href="https://codepen.io/ejinu">@ejinu</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://cpwebassets.codepen.io/assets/embed/ei.js"></script>

## Append content

\+ 버튼을 클릭 시 지정된 요소의 자식으로 HTML을 추가하고자 합니다.

먼저 버튼을 만들어줍니다.

```html
<html lang="ko">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Toggle switch</title>

    <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap@5.0.2/dist/css/bootstrap.min.css"/>
    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.0.2/dist/js/bootstrap.bundle.min.js"></script>
    <script src="https://code.jquery.com/jquery-3.6.3.min.js"></script>
</head>
<body>
    <div class="bg vw-100 vh-100 d-flex flex-column align-items-center justify-content-center">
        <div class="content-container row">
            <div class="contents"></div>
            <button type="button" id="add-btn" class="btn btn-primary border-0">+</button>
        </div>
    </div>
</body>
</html>
```

버튼과 생성되는 자식 요소를 꾸미는 css 코드를 작성해 줍니다.

```css
:root {
  --bg-color: #231F20;
  --text-color: #c7c7c7;
  --main-color: #6950A1;
  --sub-color: #EF5BA1;
}

* {
  margin: 0;
  padding: 0;
  color: var(--text-color);
}

::-webkit-scrollbar {
  width: 5px;
}

::-webkit-scrollbar-thumb {
  background: var(--sub-color);
  border-radius: 5px;
}

.bg {
  background-color: var(--bg-color);
}

.content-container {
  width: 300px;
}

.contents {
  padding: 0rem;
  max-height: 350px;
  overflow-x: hidden;
  overflow-y: auto;
}

.btn-primary {
  width: 100%;
  background-color: var(--main-color);
}

.btn-primary:hover {
  background-color: var(--sub-color);
}

.btn-primary:focus {
  box-shadow: none;
  color: var(--text-color);
  background-color: var(--sub-color);
}

.input-group {
  position: relative;
  width: 100%;
  padding: 0rem;
  margin: 1rem 0rem;
  align-items: center;
}

.input-group input {
  width: 100%;
  height: 40px;
  margin: 0px!important;
  padding: 0.5rem;
  border: 0;
  border-radius: 0.25rem!important;
  color: var(--text-color);
	background: var(--main-color);
	font-size: 1rem;
  outline: none;
}
.input-group label {
  position: absolute;
	top: 0.5rem;
	left: 1rem;
	font-size: 1rem;
  color: var(--text-color);
  transition: all 0.2s ease-in-out;
}
.input-group input:focus + label,
.input-group input:valid + label {
  top: -1.1rem;
  left: 0.1rem;
  color: var(--text-color);
  font-size: 0.7rem;
  opacity: 0.6;
}
```

버튼을 클릭 시 이벤트를 감지하여 자식 요소를 추가하도록 js 코드를 작성합니다.

```js
$("#add-btn").on("click", function() {
  var template = '' +
      '<div class="row m-0">' +
        '<div class="input-group">' +
          '<input type="text" id="data" name="data[]" required>' +
          '<label for="data">DATA</label>' +
        '</div>' +
      '</div>';
  $(".contents").append(template);
});
```

![](2023-05-09-19-32-50.gif)
_Result of append_