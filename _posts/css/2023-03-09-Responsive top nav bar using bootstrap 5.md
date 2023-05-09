---
title       : "Responsive top nav bar using bootstrap 5"
date        : 2023-03-09 16:14
categories  : [css]
tags        : [html, css, front end, bootstrap, nav]
img_path    : /assets/img/posts/css
---

## Overview

<p class="codepen" data-height="300" data-theme-id="dark" data-default-tab="result" data-slug-hash="MWqvdPJ" data-user="ejinu" style="height: 300px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;">
  <span>See the Pen <a href="https://codepen.io/ejinu/pen/MWqvdPJ">
  Top nav bar using bootstrap 5</a> by ejinu (<a href="https://codepen.io/ejinu">@ejinu</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://cpwebassets.codepen.io/assets/embed/ei.js"></script>

## Responsive top nav

Bootstrap 5를 이용할 것이기 때문에 다음의 코드를 불러옵니다.

```html
<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap@5.0.2/dist/css/bootstrap.min.css"/>
<script src="https://cdn.jsdelivr.net/npm/bootstrap@5.0.2/dist/js/bootstrap.bundle.min.js"></script>
```

992px 미만이 되면 상단 메뉴가 햄버거 버튼으로 변경되는 반응형 메뉴입니다.

```html
<nav class="navbar navbar-expand-lg navbar-dark">
    <div class="container">
      <a class="navbar-brand d-flex align-items-center" href="#">
        <img src="https://getbootstrap.com/docs/5.0/assets/brand/bootstrap-logo.svg" alt="" width="30" height="24" class="d-inline-block align-text-top">
        LOGO
      </a>
      <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarText" aria-controls="navbarText" aria-expanded="false" aria-label="Toggle navigation">
        <span class="navbar-toggler-icon"></span>
      </button>
      <div class="collapse navbar-collapse flex-grow-0" id="navbarText">
        <ul class="navbar-nav mb-2 mb-lg-0">
          <li class="nav-item">
            <a class="nav-link" href="#">MENU 1</a>
          </li>
          <li class="nav-item">
            <a class="nav-link" href="#">MENU 2</a>
          </li>
          <li class="nav-item">
            <a class="nav-link" href="#">MENU 3</a>
          </li>
          <li class="nav-item dropdown">
            <a class="nav-link dropdown-toggle" href="#" id="navbarDropdownMenuLink" role="button" data-bs-toggle="dropdown" aria-expanded="false">MENU 4</a>
            <ul class="dropdown-menu" aria-labelledby="navbarDropdownMenuLink">
              <li><a class="dropdown-item" href="#">MENU 4-1</a></li>
              <li><a class="dropdown-item" href="#">MENU 4-2</a></li>
              <li><a class="dropdown-item" href="#">MENU 4-3</a></li>
            </ul>
          </li>
        </ul>
      </div>
    </div>
</nav>
```

css는 다음과 같습니다.

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

body {
  background-color: var(--bg-color);
}

.navbar-toggler:focus {
  box-shadow: none;
}

.navbar-toggler:active {
  transform: scale(0.9);
}

.navbar {
  background-color: var(--main-color);
}

/* DROPDOWN */
.dropdown-menu {
  padding: 0px;
  background-color: var(--main-color);
  border: none;
}

.dropdown-item {
  color: rgba(255,255,255,.55);
  border: none;
}

.dropdown-item:focus, .dropdown-item:hover {
  color: rgba(255,255,255,.75);
  background-color: inherit;
}
```

![](2023-05-09-19-18-18.gif)
_Result of nav_