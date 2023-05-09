---
title       : "Toggle switch"
date        : 2023-02-21 14:25
categories  : [css]
tags        : [html, css, front end, toggle]
img_path    : /assets/img/posts/css
---

## Overview

<p class="codepen" data-height="300" data-default-tab="result" data-slug-hash="MWqKXBJ" data-user="ejinu" style="height: 300px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;">
  <span>See the Pen <a href="https://codepen.io/ejinu/pen/MWqKXBJ">
  toggle switch</a> by ejinu (<a href="https://codepen.io/ejinu">@ejinu</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://cpwebassets.codepen.io/assets/embed/ei.js"></script>

## Toggle switch

어두운 모드와 밝은 모드를 변경하는 버튼 형식의 토글 스위치를 만들어 줍니다.

```html
<html lang="ko">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Toggle switch</title>

    <script src="https://code.jquery.com/jquery-3.6.1.min.js"></script>
</head>
<body>
    <div class="toggle-switch-container">
        <div class="toggle-switch"><div class="switch"></div></div>
    </div>
</body>
</html>
```

default 색상을 지정하고 토글 스위치의 크기를 지정하여 화면에 렌더링 해줍니다.

```css
:root {
  --bg-color: #231F20;
  --text-color: #c7c7c7;
  --main-color: #6950A1;
}

* {
  margin: 0;
  padding: 0;
}

body {
  width: 100vw;
  height: 100vh;
  display: flex;
  align-items: center;
  justify-content: center;
  background-color: var(--bg-color);
}

.toggle-switch-container {
  margin: 0px;
  display: flex;
  align-items: center;
  justify-content: end;
}

.toggle-switch-container > .toggle-switch {
  cursor: pointer;
  width: 70px;
  height: 30px;
  background: var(--main-color);
  border-radius: 50px;
  position: relative;
}

.toggle-switch-container > .toggle-switch > .switch {
  background: var(--bg-color);
  width: 24px;
  height: 24px;
  border-radius: 100%;
  position: absolute;
  top: 3px;
  left: 4px;
  transition: 0.5s all ease;
}
```

![](2023-05-09-17-55-37.png)
_Result of toggle switch_

## Theme

default 색상을 지정하였다면, 스위치를 클릭 시 변경될 색상을 지정해 줍니다.

또한, 변화를 알아볼 수 있게 스위치의 위치를 이동시켜줍니다.

```css
body.light {
  --bg-color: #c7c7c7;
}

.light .toggle-switch-container > .toggle-switch > .switch {
  transform: translateX(37px);
}
```

색상을 지정하였다면, 스위치에 클릭 이벤트를 지정하여 클릭 시 body 태그에 class를 추가하는 js 코드를 작성합니다.

```html
<body>
    <div class="toggle-switch-container">
        <div class="toggle-switch"><div class="switch"></div></div>
    </div>
    <script>
        $(".toggle-switch").on("click", () => {
            $("body").toggleClass("light");
        });
    </script>
</body>
```

스위치를 클릭하면 body에 light class가 추가되고, body.light 색상에 따라

각 요소들의 색상이 변화됩니다.

![](2023-05-09-18-03-01.png)
_Result of toggle switch_