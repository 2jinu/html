---
title       : "Code editor using Ace"
date        : 2023-05-08 20:32
categories  : [js]
tags        : [code editor, ace]
img_path    : /assets/img/posts/js
---

## Overview

<p class="codepen" data-height="300" data-default-tab="result" data-slug-hash="vYVZGJX" data-user="ejinu" style="height: 800px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;">
  <span>See the Pen <a href="https://codepen.io/ejinu/pen/vYVZGJX">
  Ace editor with bootstrap 5</a> by ejinu (<a href="https://codepen.io/ejinu">@ejinu</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://cpwebassets.codepen.io/assets/embed/ei.js"></script>

## Ace

[Ace](https://ace.c9.io/)를 이용하면 웹 브라우저 상에서 시각적으로 코드를 보기 좋게 볼 수 있고, 작성할 수 있습니다.

다양한 언어 및 테마와 기능들을 제공합니다.

다음은 python 코드 편집기에 대한 예시입니다.

```html
<html lang="ko">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Code Editor</title>

    <script src="https://cdnjs.cloudflare.com/ajax/libs/ace/1.9.6/ace.min.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/ace/1.9.6/mode-python.min.js"></script>

    <style>
        #editor {
            position: absolute;
            width: 500px;
            height: 400px;
        }
    </style>
</head>
<body>
    <div id="editor"></div>
</body>

<script>
    var editor = ace.edit("editor");
    editor.session.setMode("ace/mode/python");
    editor.setValue('# Write Python 3 code in this editor and run it.\r\n\r\ndef greeting():\r\n    print("Hello World!")\r\n\r\ngreeting()', 1);
</script>
</html>
```

렌더링된 결과는 다음과 같습니다.

![](2023-05-08-20-14-59.png)
_Result of Ace_

## Theme

기본 테마는 `밝은(Light)` 모드입니다. 원하는 테마를 로드한 뒤, `setTheme`를 이용하여 코드 편집기의 색상을 변경할 수 있습니다.

다음은 theme-tomorrow_night_bright를 적용한 예시입니다.

```html
<head>
    ... 생략
    <script src="https://cdnjs.cloudflare.com/ajax/libs/ace/1.9.6/theme-tomorrow_night_bright.min.js"></script>
    ... 생략
</head>
<body>
    <div id="editor"></div>
</body>

<script>
    var editor = ace.edit("editor");
    editor.setTheme("ace/theme/tomorrow_night_bright");
    editor.session.setMode("ace/mode/python");
    editor.setValue('# Write Python 3 code in this editor and run it.\r\n\r\ndef greeting():\r\n    print("Hello World!")\r\n\r\ngreeting()', 1);
</script>
```

결과를 확인해 봅니다.

![](2023-05-08-20-20-46.png)
_Result of Ace_

## Options

다양한 [옵션](https://ace.c9.io/#nav=howto)들이 존재하지만

폰트 크기(setFontSize), 들여쓰기(setTabSize), 활성화된 줄 강조(setHighlightActiveLine) 기능을 사용해 봅니다.

```js
var editor = ace.edit("editor");
editor.setTheme("ace/theme/tomorrow_night_bright");
editor.session.setMode("ace/mode/python");

editor.setFontSize("14px");
editor.session.setTabSize(4);
editor.setHighlightActiveLine(true);

editor.setValue('# Write Python 3 code in this editor and run it.\r\n\r\ndef greeting():\r\n    print("Hello World!")\r\n\r\ngreeting()', 1);
```

결과를 확인해 봅니다.

![](2023-05-08-20-23-19.png)
_Result of Ace_

## Autocompletion

VSCode의 Extensions 만큼 코드 자동완성을 지원하지는 않지만

몇몇 매우 기본적인 문법은 자동완성을 지원하는 기능이 있습니다.

필요한 js 코드를 불러오고, `enableSnippets`와 `enableLiveAutocompletion`를 활성화해 줍니다.

다음은 python의 if __name__ == '__main__': 에 대한 자동완성 예시입니다.

```html
<head>
    ... 생략
    <script src="https://cdnjs.cloudflare.com/ajax/libs/ace/1.9.6/ext-language_tools.min.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/ace/1.9.6/snippets/python.min.js"></script>
    ... 생략
</head>
<body>
    <div id="editor"></div>
</body>

<script>
    var editor = ace.edit("editor");
    editor.setTheme("ace/theme/tomorrow_night_bright");
    editor.session.setMode("ace/mode/python");
    editor.setOptions({copyWithEmptySelection: false, showGutter: true, showLineNumbers: true, enableBasicAutocompletion: false, enableSnippets: true, enableLiveAutocompletion: true});
    editor.setValue('# Write Python 3 code in this editor and run it.\r\n\r\ndef greeting():\r\n    print("Hello World!")\r\n\r\ngreeting()', 1);
</script>
```

결과를 확인해 봅니다.

![](2023-05-08-20-31-36.png)
_Result of Ace_