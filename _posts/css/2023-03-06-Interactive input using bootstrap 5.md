---
title       : "Interactive input using bootstrap 5"
date        : 2023-03-06 11:34
categories  : [css]
tags        : [html, css, front end, bootstrap, input]
img_path    : /assets/img/posts/css
---

## Overview

<p class="codepen" data-height="500" data-theme-id="dark" data-default-tab="result" data-slug-hash="jOvLMKo" data-user="ejinu" style="height: 300px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;">
  <span>See the Pen <a href="https://codepen.io/ejinu/pen/jOvLMKo">
  Input Style 1</a> by ejinu (<a href="https://codepen.io/ejinu">@ejinu</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://cpwebassets.codepen.io/assets/embed/ei.js"></script>

## Common Required

Bootstrap 5와 Font Awesome을 이용하여 간편하게 디자인합니다.

비밀번호의 규칙과 비밀번호 보이기 버튼 등 동적인 처리를 위하여 jQuery를 로드해 줍니다.

```html
<html lang="ko">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Toggle switch</title>

    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.3.0/css/all.min.css"/>
    <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap@5.0.2/dist/css/bootstrap.min.css"/>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.3.0/js/all.min.js"></script>
    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.0.2/dist/js/bootstrap.bundle.min.js"></script>
    <script src="https://code.jquery.com/jquery-3.6.3.min.js"></script>
</head>
<body>
</body>
</html>
```

## Text

input 태그의 placeholder 요소 대신에 label을 이용하여 무엇을 입력해야 하는지 사용자를 유도하며

input 태그를 `클릭(focus)`하거나 데이터를 `입력(valid)`하면 label의 위치를 옮겨

입력된 데이터를 가리지 않게 합니다.

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

.bg {
    min-width: 250px;
    background-color: var(--bg-color);
}

.input-group {
    position: relative;
    width: 300px;
    align-items: center;
    margin: 0.9rem 0;
}
.input-group input {
    width: 100%;
    height: 40px;
    margin: 0px!important;
    padding: 0.5rem;
    border: 0;
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
.input-group input:focus + label, .input-group input:valid + label {
    top: -1.1rem;
    left: 0.1rem;
    color: var(--text-color);
    font-size: 0.7rem;
    opacity: 0.6;
}
```

텍스트를 받을 수 있는 input을 정의해 줍니다.

```html
<div class="bg vw-100 vh-100 d-flex flex-column align-items-center justify-content-center">
    <div class="input-group">
        <input type="text" class="rounded-3" id="name" required>
        <label for="name">NAME</label>
    </div>
</div>
```

![](2023-05-09-18-41-01.gif)
_Result of input text_

## Search

검색 모양으로 쓰이는 돋보기 아이콘을 이용한 버튼을 만들어주어 검색 창으로 표현해 봅니다.

```css
.search-btn {
    width: 40px;
    height: 40px;
    background: var(--sub-color);
    color: var(--text-color);
    cursor: pointer;
}
```

텍스트를 받을 수 있는 input을 정의해 줍니다.

```html
<div class="bg vw-100 vh-100 d-flex flex-column align-items-center justify-content-center">
    <div class="input-group flex-nowrap">
        <input type="text" class="rounded-start" placeholder="Search the name...">
        <button type="submit" class="search-btn border-0 rounded-end">
            <i class="fa fa-search"></i>
        </button>
    </div>
</div>
```

![](2023-05-09-19-04-43.gif)
_Result of input Search_

## Datetime

input text와 같은 css를 공유하며 `-webkit-calendar-picker-indicator`에 대한 색 반전을 시켰습니다. 기본색은 검은색입니다.

```css
::-webkit-calendar-picker-indicator {
    cursor: pointer;
    filter: invert(1);
}
```

시간을 받을 수 있는 input을 정의해 줍니다.

```html
<div class="bg vw-100 vh-100 d-flex flex-column align-items-center justify-content-center">
    <div class="input-group">
        <input type="datetime-local" class="rounded-3" id="datetime" name="datetime">
        <label for="datetime">DATETIME</label>
    </div>
</div>
```

![](2023-05-09-18-45-11.gif)
_Result of input datetime_

## Password

input text에 추가적인 수정이 필요하여 css를 작성합니다.

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

.bg {
    min-width: 250px;
    background-color: var(--bg-color);
}

.input-group {
    position: relative;
    width: 300px;
    align-items: center;
    margin: 0.9rem 0;
}
.input-group input {
    width: 100%;
    height: 40px;
    margin: 0px!important;
    padding: 0.5rem;
    border: 0;
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
.input-group input:focus + label, .input-group input:valid + label {
    top: -1.1rem;
    left: 0.1rem;
    color: var(--text-color);
    font-size: 0.7rem;
    opacity: 0.6;
}

strong {
    color: inherit;
}
.input-group.password-input {
    margin: 0rem 0rem 0.7rem 0rem;
}
.password-input span {
    font-size: 0.8rem;
}
.password-input input {
    padding-right: 2.5rem;
}
.password-input label {
    top: 1.7rem;
}
.password-input input:focus + label, .password-input input:valid + label {
    top: 0rem;
}
.password-input .eye {
    position: absolute;
    top: 0.6rem;
    width: 35px;
    cursor: pointer;
}
::-ms-reveal {
  display: none;
}
```

비밀번호에 input 요소에 키가 입력되는 이벤트를 받아서 비밀번호 정책을 검사하는 함수와 비밀번호 재입력에 대한 검사를 진행합니다.

우측 눈 모양의 아이콘을 누르면 password 타입에서 text 타입으로 변하게 되어 비밀번호를 문자열로 확인할 수 있습니다.

```js
$("#password").keyup(function() {
  var password = $(this).val();

  var lowerCaseLetters = /[a-z]/g;
  var upperCaseLetters = /[A-Z]/g;
  var numbers = /[0-9]/g;
  
  if(password.match(lowerCaseLetters)) {
    if(password.match(upperCaseLetters)) {
      if(password.match(numbers)) {
        if(password.length >= 8) {
          $("#password-policy").html("Success");
          $("#password-policy").removeClass("text-danger");
          $("#password-policy").addClass("text-success");
        } else {
          $("#password-policy").html("At least <strong>8 characters</strong>");
          $("#password-policy").addClass("text-danger");
          $("#password-policy").removeClass("text-success");
        }
      } else {
        $("#password-policy").html("At least 1 <strong>Number</strong>");
        $("#password-policy").addClass("text-danger");
         $("#password-policy").removeClass("text-success");
      }
    } else {
      $("#password-policy").html("At least 1 <strong>upper</strong> letter");
      $("#password-policy").addClass("text-danger");
      $("#password-policy").removeClass("text-success");
    }
  } else {
    $("#password-policy").html("At least 1 <strong>lower</strong> letter");
    $("#password-policy").addClass("text-danger");
    $("#password-policy").removeClass("text-success");
  }
  
  var confirm = $("#password-confirm").val();
  
  if (confirm === "") {
    $("#password-check").html("Empty");
    $("#password-check").addClass("text-danger");
    $("#password-check").removeClass("text-success");
  }
  else if (confirm !== password) {
    $("#password-check").html("Not matched");
    $("#password-check").addClass("text-danger");
    $("#password-check").removeClass("text-success");
  } else {
    $("#password-check").html("Matched");
    $("#password-check").removeClass("text-danger");
    $("#password-check").addClass("text-success");
  }
});

$("#password-eye").on( "click", function() {
  const type = $("#password").attr('type') === 'password' ? 'text' : 'password';
  $("#password").attr('type', type);
  $(this).children("svg").toggleClass('fa-eye-slash fa-eye');
});

$("#password-confirm").keyup(function() {
  var password = $("#password").val();
  var confirm = $(this).val();
  
  if (confirm === "") {
    $("#password-check").html("Empty");
    $("#password-check").addClass("text-danger");
    $("#password-check").removeClass("text-success");
  }
  else if (confirm !== password) {
    $("#password-check").html("Not matched");
    $("#password-check").addClass("text-danger");
    $("#password-check").removeClass("text-success");
  } else {
    $("#password-check").html("Matched");
    $("#password-check").removeClass("text-danger");
    $("#password-check").addClass("text-success");
  }
});

$("#password-confirm-eye").on( "click", function() {
  const type = $("#password-confirm").attr('type') === 'password' ? 'text' : 'password';
  $("#password-confirm").attr('type', type);
  $(this).children("svg").toggleClass('fa-eye-slash fa-eye');
});
```

비밀번호를 받을 수 있는 input을 정의해 줍니다.

```html
<div class="bg vw-100 vh-100 d-flex flex-column align-items-center justify-content-center">
    <div class="input-group password-input text-end">
        <span class="w-100 text-danger" id="password-policy">At least 1 <strong>lower</strong> letter</span>
        <input type="password" class="rounded-3" id="password" required>
        <label for="password">PASSWORD</label>
        <div class="eye d-flex align-items-center justify-content-center h-100 end-0" id="password-eye">
            <i class="fa-regular fa-eye"></i>
        </div>
    </div>

    <div class="input-group password-input text-end">
        <span class="w-100 text-danger" id="password-check">Empty</span>
        <input type="password" class="rounded-3" id="password-confirm" required>
        <label for="password-confirm">PASSWORD CONFIRM</label>
        <div class="eye d-flex align-items-center justify-content-center h-100 end-0" id="password-confirm-eye">
            <i class="fa-regular fa-eye"></i>
        </div>
    </div>
</div>
```

![](2023-05-09-18-58-41.gif)
_Result of input password_