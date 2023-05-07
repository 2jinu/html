---
title       : "Hierarchical folder tree"
date        : 2023-05-07 19:53
categories  : [js]
tags        : [jstree, dnd, contextmenu, tree]
img_path    : /assets/img/posts/js
---

## jsTree

[jsTree](https://www.jstree.com/)를 이용하면 웹 브라우저 상에서 다양한 기능을 제공하는 폴더 트리를 구현할 수 있습니다.

[jQuery](https://releases.jquery.com/)와 [소스 코드](https://github.com/vakata/jstree/)를 다운로드하여 `dist` 폴더에서 소스코드를 불러와봅니다.

```html
<html lang="ko">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>jsTree</title>

    <script src="https://code.jquery.com/jquery-3.6.4.min.js" integrity="sha256-oP6HI9z1XaZNBrJURtCoUT5SUnxFr8s3BzRl+cbzUq8=" crossorigin="anonymous"></script>
    <script src="/dist/jstree.min.js"></script>
    <link rel="stylesheet" href="/dist/themes/default/style.min.css"/>
</head>
<body>
</body>
</html>
```

이제 데이터를 통해 계층적인 폴더 트리를 만들어봅니다.

다음의 코드는 Root라는 최상위 노드에서 2개의 Child 노드가 포함되는 구조입니다.

```html
<body>
    <div id="tree"></div>
    <script>
        $('#tree').jstree({
            'core' : {
                'data' : [
                    {
                        'text' : 'Root',
                        'children' : [
                            { 'text' : 'Child1' },
                            { 'text' : 'Child2' }
                        ]
                    }
                ]
            }
        });
    </script>
</body>
```

렌더링된 결과는 다음과 같습니다.

![](2023-05-07-20-36-13.png)
_Result of jsTree_

### State

노드 별 `state` 속성을 전달하여 `오픈 상태(opened)`, `선택 상태(selected)`, `활성 여부(disabled)`를 적용할 수 있습니다.

```js
'data' : [
    {
        'text' : 'Root',
        'state' : {'opened' : true },
        'children' : [
            { 'text' : 'Child1', 'state' : { 'selected' : true } },
            { 'text' : 'Child2', 'state' : { 'disabled' : true } }
        ]
    }
]
```

### Data

data를 url를 통해서 얻어오고 싶다면 다음과 같이 사용할 수 있습니다.

```js
'core' : {
    'data' : {
        "url" : "//www.jstree.com/fiddle/",
        "dataType" : "json"
    }
}
```

## Type

jsTree에서는 노드 별 타입을 구별할 수 있는 `types` 플러그인을 제공합니다.

노드 별 타입을 구별하기 위해 `plugins`에 types를 전달하고 노드의 속성에 type을 지정합니다.

`types`에는 타입 별 아이콘 및 속성들을 지정할 수 있습니다.

다음은 기본적으로 제공하는 `jstree-folder`와 `jstree-file`을 사용하였습니다.

별도의 아이콘이 필요하다면 클래스 명으로 지정하거나 아이콘 이미지의 경로를 지정하여 사용할 수 있습니다.

```js
$('#tree').jstree({
    'plugins': ['types'],
    'core' : {
        'data' : [
            {
                'text' : 'Root',
                'type' : 'directory',
                'children' : [
                    { 'text' : 'Child1', 'type' : 'file' },
                    { 'text' : 'Child2', 'type' : 'file' }
                ]
            }
        ]
    },
    'types': {
        "directory": { 'icon': 'jstree-folder' },
        "file": { "icon": 'jstree-file' }
    }
});
```

렌더링된 결과는 다음과 같습니다.

![](2023-05-07-20-50-25.png)
_Result of jsTree_

## DnD

폴더 구조라면 `DnD(Drag and Drop)` 기능은 빼놓을 수 없다. 따라서 jsTree에서도 `dnd` 플러그인을 제공합니다.

노드의 이동을 위해 `plugins`에 `dnd`를 전달하고 노드의 속성에 type을 지정합니다.

이벤트가 처리되기 위해서는 `check_callback`의 반환 값이 `true`가 되어야 합니다.

폴더는 파일 및 폴더를 포함할 수 있지만, 파일은 그럴 수 없기 때문에 파일 타입 속성에 `valid_children`을 지정합니다.

Draggable nested tree를 실습하기 위해서 다양한 구조의 데이터를 넣어서 확인해 봅니다.

```js
$('#tree').jstree({
    'plugins': ['types', 'dnd'],
    'core' : {
        'check_callback': true,
        'data' : [
            {
                'text' : 'Folder1',
                'type' : 'directory',
                'state' : {'opened' : true },
                'children' : [
                    { 'text' : 'File1', 'type' : 'file', 'state' : { 'selected' : true } },
                    { 'text' : 'File2', 'type' : 'file', 'state' : { 'disabled' : true } }
                ]
            },
            {
                'text' : 'Folder2',
                'type' : 'directory',
                'state' : {'opened' : true },
                'children' : [
                    {
                        'text' : 'Folder3',
                        'type' : 'directory',
                        'state' : { 'opened' : true },
                        'children' : [ { 'text' : 'File3', 'type' : 'file' } ]
                    },
                    { 'text' : 'File4', 'type' : 'file' }
                ]
            }
        ]
    },
    'types': {
        "directory": { 'icon': 'jstree-folder' },
        "file": { "icon": 'jstree-file', "valid_children": [] }
    }
});
```

렌더링된 결과는 다음과 같습니다.

![](2023-05-07-21-06-19.png)
_Result of jsTree_

## Contextmenu

폴더 및 파일을 생성하고 싶다면 jsTree의 `contextmenu` 플러그인을 사용합니다.

기본 값으로는 tree 요소 안에서 `우클릭`을 통해 `Create`, `Rename`, `Delete`, `Cut`, `Copy` 기능을 사용할 수 있습니다.

```js
'plugins': ['types', 'dnd', 'contextmenu'],
```

마우스의 오른쪽 버튼을 클릭해 보면 contextmenu가 나오고

다양한 메뉴들을 클릭해 봅니다.

![](2023-05-07-21-11-11.png)
_Result of jsTree_

폴더와 파일을 다루고 있지만 Create는 `폴더만 생성`하고 있는 문제점이 존재합니다.

따라서, 사용자 정의 메뉴로 contextmenu의 메뉴를 교체해 봅니다.

Create 메뉴에서 `파일`과 `폴더`를 `구별하여 생성하는 기능`을 만들어 봅니다.

```js
$('#tree').jstree({
    'plugins': ['types', 'dnd', 'contextmenu'],
    'core' : {
        'check_callback': true,
        'data' : [
            {
                'text' : 'Folder1',
                'type' : 'directory',
                'state' : {'opened' : true },
                'children' : [
                    { 'text' : 'File1', 'type' : 'file', 'state' : { 'selected' : true } },
                    { 'text' : 'File2', 'type' : 'file', 'state' : { 'disabled' : true } }
                ]
            },
            {
                'text' : 'Folder2',
                'type' : 'directory',
                'state' : {'opened' : true },
                'children' : [
                    {
                        'text' : 'Folder3',
                        'type' : 'directory',
                        'state' : { 'opened' : true },
                        'children' : [ { 'text' : 'File3', 'type' : 'file' } ]
                    },
                    { 'text' : 'File4', 'type' : 'file' }
                ]
            }
        ]
    },
    'types': {
        "directory": { 'icon': 'jstree-folder' },
        "file": { "icon": 'jstree-file', "valid_children": [] }
    },
    "contextmenu": {
        "items": function ($node) {
            var tree = $('#tree').jstree(true);
            return {
                "Create": {
                    "separator_before": false,
                    "separator_after": true,
                    "label": "Create",
                    "action": false,
                    "submenu": {
                        "File": {
                            "seperator_before": false,
                            "seperator_after": false,
                            "label": "File",
                            action: function (obj) {
                                $node = tree.create_node($node, { text: 'NewFile', type: 'file' });
                                tree.deselect_all();
                                tree.select_node($node);
                            }
                        },
                        "Directory": {
                            "seperator_before": false,
                            "seperator_after": false,
                            "label": "Directory",
                            action: function (obj) {
                                $node = tree.create_node($node, { text: 'NewFolder', type: 'directory' });
                                tree.deselect_all();
                                tree.select_node($node);
                            }
                        }
                    }
                },
                "Rename": {
                    "separator_before": false,
                    "separator_after": false,
                    "label": "Rename",
                    "action": function (obj) {
                        tree.edit($node);                                    
                    }
                },
                "Remove": {
                    "separator_before": false,
                    "separator_after": false,
                    "label": "Remove",
                    "action": function (obj) {
                        tree.delete_node($node);
                    }
                }
            };
        }
    }
});
```

마우스의 오른쪽 버튼을 클릭하여 기능들을 확인해 봅니다.

![](2023-05-07-21-16-49.png)
_Result of jsTree_

## Sort and Unique

같은 폴더에서는 동일한 파일 명을 생성할 수 없지만 현재 상태에서는 같은 파일을 생성할 수 있습니다.

또한, 노드의 이름(text)를 기준으로 정렬되는 기능을 사용하기 위해 `sort`와 `unique` 플러그인을 사용합니다.

```js
'plugins': ['types', 'dnd', 'contextmenu', 'sort', 'unique'],
```

## Theme

기본 테마는 `밝은(Light)` 모드입니다. `themes` 플러그인을 추가한 뒤 jsTree의 소스코드에서

dist 폴더에서 default-dark를 사용하여 `어두운(Dark)` 모드를 사용해 봅니다.

```html
<html lang="ko">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>jsTree</title>

    <script src="https://code.jquery.com/jquery-3.6.4.min.js" integrity="sha256-oP6HI9z1XaZNBrJURtCoUT5SUnxFr8s3BzRl+cbzUq8=" crossorigin="anonymous"></script>
    <script src="/dist/jstree.min.js"></script>
    <link rel="stylesheet" href="/dist/themes/default/style.min.css"/>
    <link rel="stylesheet" href="/dist/themes/default-dark/style.min.css"/>
</head>
<body>
    <div id="tree"></div>
    <script>
        $('#tree').jstree({
            'plugins': ['types', 'dnd', 'contextmenu', 'sort', 'unique', 'themes'],
            'core' : {
                'themes':{
                    'name':'default-dark',
                    'icons':true,
                    'dots':true
                },
    ... 생략
```

결과를 확인해 봅니다.

![](2023-05-07-21-34-37.png)
_Result of jsTree_

토글 버튼 등으로 테마를 변경하고자 한다면 다음과 같은 api를 사용합니다.

```js
$('#tree').jstree("set_theme","default-dark"); // dark mode
$('#tree').jstree("set_theme","default"); // light mode
```

## Callback

jsTree를 이용하면 노드를 생성하고 삭제하고 이동하는 등의 기능을 사용할 수 있습니다.

생성 및 삭제 등의 이벤트가 발생하였을 때, 추가적인 기능을 수행하거나 해당 기능 자체를 막거나 하고 싶을 수 있습니다.

이때, `check_callback`을 이용하여 해결합니다.

다음은 삭제 기능에 대한 이벤트(delete_node)를 처리하는 예제입니다.

노드를 삭제 시 재확인을 요구하고 취소 버튼을 클릭 시 false를 반환하여 기능이 수행되지 않습니다.

```js
'check_callback': function(operation, node, node_parent, node_position, more) {
      if (operation == "delete_node") {
          var confirmDelete = confirm(`Are you sure to delete ${node.text}?`);
          if (!confirmDelete) return false;
      }
      return true;
  }
```

check_callback이 먼저 처리되고 이벤트 리스너로 핸들링해 봅니다.

다음은 노드를 클릭 시(select_node)에 대한 이벤트를 처리하는 예제이며,

클릭의 타입이 좌클릭이며 클릭 대상이 파일일 때, alert가 출력됩니다.

```js
$('#tree').jstree({
  ...
});

$("#tree").on('select_node.jstree', function (e, d) {
    try {
        if (d.event.type == "click" && d.node.type === 'file') {
            alert(d.node.text + ' is file');
        }
    } catch (e) {
        console.log(e);
    }
});
```