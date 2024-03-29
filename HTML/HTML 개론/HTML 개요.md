## HTML 개요

HTML(Hypertext Markup Language)은 흔히 말하는 프로그래밍 언어가 아닙니다. 웹 페이지라는 문서에 마크업을 하기 위한 언어 또는 구문입니다.

웹 페이지는 단순한 코드로 구성되어 있습니다. 즉, 단순한 정보이자 텍스트를 의미합니다. 그러나 이 텍스트 안에는 브라우저가 알아야 할 모든 페이지의 구조와 규칙이 들어 있습니다. 또한 HTML이 규칙을 알기 때문에 화면이 렌더링되어 출력됩니다.

이런 규칙과 구조들은 HTML이 논문으로 발표된 이후 학술 연구자들이 연구 보고서를 공유하며 어떻게 만들지 고민했습니다. 실생활에서 텍스트를 마크업하는 방법은 여러 가지입니다. 만약 "Hello HTML" 라는 문장에서 "Hello" 부분만 이탤릭체로 표시하고 싶다면 많은 방법 중에 하나로 "(이탤릭체) => Hello HTML" 로 나타낼 수도 있을겁니다.

하지만 HTML에 존재하는 텍스트를 마크업하는 방법은 전세계에서 사용해야 하기 때문에 통일할 필요성이 있었습니다. 따라서 등장하게 된 개념이 HTML 요소(HTML ELEMENTS)입니다. HTML 요소는 이미지 요소, 양식 요소, 굵은 글씨, 이탤릭체 등 많은 요소가 있지만 일반적인 패턴이 있는 태그 구문을 쓰면 어렵지 않습니다. 태그로 텍스트를 감싸면 끝입니다.

```html
<!-- 단순 본문을 나타낼 경우 -->
<p>I am a paragraph</p>
<!-- 이탤릭체를 사용할 경우 -->
<i>Hello</i> HTML
```

여기서 `<p>`는 시작 태그, `</p>`는 종료 태그라 부릅니다. 시작 태그가 있으면 무조건 종료 태그가 존재해야 합니다. 만약 종료 태그로 닫지 않는다면 HTML은 어디서 태그를 종료해야 할지 모르기 때문에 문서 전체에 요소가 적용되거나 에러가 발생할 수도 있습니다.

정리하자면 HTML은 이런 식으로 HTML 요소를 조합하여 문서에 마크업을 합니다. 웹 문서를 태그로 마크업하면 우리가 흔히 볼 수 있는 웹 페이지가 출력될 수 있는 이유입니다.
