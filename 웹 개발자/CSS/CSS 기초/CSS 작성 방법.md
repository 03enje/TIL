## CSS 작성 방법

CSS 작성 방법에는 인라인 스타일, 스타일(\<style>) 요소, 외부 스타일 시트로 총 3가지 방법이 있습니다.

## 인라인 스타일(Inline styles)

HTML 요소에 직접 스타일을 작성합니다. 인라인 스타일의 경우 같은 그룹 요소에 동일한 스타일을 지정하고 싶을 경우가 있을 때 작업에 많은 시간이 소요되므로 추천되지 않는 방법입니다.

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>CSS Intro</title>
  </head>
  <body>
    <h1 style="color: purple">Hello World</h1>
    <button style="background-color: palegreen">I AM BUTTON</button>
    <button style="background-color: palegreen">Another button!</button>
  </body>
</html>
```

## 스타일 요소(\<style>)

HTML 상용구 \<head> 에 \<style>을 기입하여 작성합니다.

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>CSS Intro</title>
    <style>
      h2 {
        color: palevioletred;
      }
    </style>
  </head>
  <body>
    <h2>I am an h2</h2>
    <h2>I am an h2</h2>
    <h2>I am an h2</h2>
  </body>
</html>
```

## 외부 스타일 시트(External style sheet)

외부 스타일 시트에서 스타일을 작성하는 방법입니다. .css 확장자를 가진
파일을 HTML \<link> 태그에 포함시켜 사용합니다.

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>CSS Intro</title>
    <link rel="stylesheet" href="app.css" />
  </head>
  <body>
    <h2>I am an h2</h2>
  </body>
</html>
```

```css
/** app.css */
h2 {
  color: indigo;
}
```
