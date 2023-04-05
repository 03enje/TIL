## CSS

CSS는 캐스케이딩 스타일 시트의 약자입니다. 스타일 시트는 명칭 그대로 이해할 수 있는 내용이 담긴 형식입니다. 스타일을 정하고 시각적으로 보이는 형태를 만듭니다.

페이지에 입력된 HTML 콘텐츠를 시각적으로 표현합니다.CSS를 비유하자면 다음과 같습니다.

```md
보라색 공룡이 춤을 추고 있다.

보라색(CSS) 공룡(HTML) 춤(JS)
```

## CSS 규칙

매 특성 선언(property declaration)의 끝에 붙는 세미콜론(;)은 필수 사항입니다. 만약 세미콜론을 안적으면 에러가 발생하지는 않지만 실제로 동작은 하지 않습니다.

```css
selector {
  property: value;
}

/* 예시 */
h1 {
  color: purple;
}
```

## CSS 적용 방법

### 인라인 스타일

```html
<button style="background-color: palegreen">I AM Button</button>
```

### 내부 스타일

```html
<head>
  <style>
    h2 {
      color: palevioletred;
    }
  </style>
</head>
<body>
  <h2>Hello world!</h2>
</body>
```

### 외부 스타일

rel은 관계(relationship)를 뜻하며, 현재 문서와 연결한 아이템의 관계가 어떻게 되는지 설명합니다.

```css
/* my_styles.css */
div {
  border: 1px solid black;
}
```

```html
<head>
  <link rel="stylesheet" href="my_styles.css" />
</head>
<body>
  <div>Round</div>
</body>
```
