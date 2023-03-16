## CSS란?

CSS는 캐스케이딩 스타일 시트입니다. 스타일 시트는 명칭 그대로 내용이 담긴 형식을 말합니다.

### 💡 CSS(Cascading Style Sheets)에서 캐스케이딩(Cascading)의 의미는?

> css의 스타일 속성들은 DOM 문서 트리에서 상위 앨리먼트에 있는 스타일 속성이 그 하위 앨리먼트로 흘려내려서 상속되기 때문입니다. (전부 상속된다는 소리는 아닙니다)
>
> 최상위 노드부터 아래로 스타일 속성들이 쭉 흘려내려(상속되어)가는 모습이 마치 폭포처럼 보이기 때문입니다.
>
> 폭포란게 무조건 다 흘러내려가는 것도 아니기 때문에 일부만 상속되는 것과 유사한 점 중 하나겠네요.

CSS는 문서를 시각적으로 표현하고 나타내기 위해서 사용하는 언어라 볼 수 있습니다. CSS의 예시를 보여주는 사이트<sup>[1]</sup>를 찾아가면 자세하게 살펴볼 수 있습니다.

## CSS 규칙(rules)

```css
/** CSS 기본 형태 */
selector {
  property: value;
}

/** h1 요소로 만든 CSS 예제 */
h1 {
  color: purple;
}

/** 속성 2개를 가지는 CSS */
img {
  width: 100px;
  height: 200px;
}

/** input 요소에서 text 타입을 가지는 텍스트를 2n개로 선택하여 적용 */
input[type='text']:nth-of-type(2n) {
  border: 2px solid red;
}
```

[1]: https://codepen.io/TurkAysenur/pen/JjGKKrP
