## 유효성 검사

유효성 검사는 일반적으로 제한을 추가하거나 사용자 입력 또는 데이터의 유효성을 확인합니다.

회원가입 등 폼 데이터를 폼에 제출할 때 예전에는 서버 측에서 주로 유효성 검사를 하였습니다. 하지만 점차적으로 브라우저나 클라이언트 측에서도 유효성 검사를 시행하고 있는 중 입니다.

## HTML5 폼 빌트인 유효성 검사(내장 유효성 검사)

빌트인(내장) 유효성 검사는 대다수 브라우저에서 지원하는 옵션입니다. 폼 태그 안에서 폼 컨트롤에 required 속성을 사용하면 필수적으로 값을 입력해야 하며 minlength, maxlength로 값의 길이를 제한할 수 있습니다.

몇몇 입력에는 유효성 검사가 디폴트로 내장돼어 있습니다. 대표적으로 패턴이 있는 경우가 그렇습니다. 패턴은 사실상 속성을 의미하며 두 개의 요소를 추가하고 정규 표현식이라 부릅니다. email, URL 타입 등은 기본적인 패턴이 제공되는 형태입니다.

```html
<h2>Validations Demo</h2>
<form action="/dummy">
  <label for="first">Enter First Name</label>
  <input type="text" name="first" id="first" required />
  <p>
    <label for="username">Username</label>
    <input
      type="text"
      id="username"
      name="username"
      minlength="5"
      maxlength="20"
      required
    />
  </p>
  <p>
    <!-- 기본적으로 패턴이 제공되는 타입 -->
    <input type="email" required>
    <input type="url">
  </p>
  <button>Submit</button>
</form>
```
