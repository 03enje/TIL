# CSS(Cascading Style Sheets)
HTML이나 XML로 작성된 문서의 표시 방법을 기술하기 위한 스타일 시트(style sheets) 언어

## 목차
1. [📂 How To](#-1-How-To)
   - [📄 인라인 스타일](#-인라인-스타일)
   - [📄 내부 스타일](#-내부-스타일)
   - [📄 외부 스타일](#-외부-스타일)
2. [📂 선택자](#-2-선택자)
   - [📄 태그 선택자](#-태그-선택자)
   - [📄 아이디 선택자](#-아이디-선택자)
   - [📄 클래스 선택자](#-클래스-선택자)
3. [📂 기본 속성](#-3-기본-속성)
   - [📄 텍스트 속성](#-텍스트-속성)
   - [📄 폰트 속성](#-폰트-속성)
   - [📄 링크 속성](#-링크-속성)
   - [📄 배경 속성](#-배경-속성)
   - [📄 목록 속성](#-목록-속성)
4. [📂 박스 모델](#-4-박스-모델)
   - [📄 콘텐츠](#-콘텐츠content)
   - [📄 패딩](#-패딩padding)
   - [📄 테두리](#-테두리border)
   - [📄 마진](#-마진margin)
5. [📂 디스플레이](#-5-디스플레이)
   - [📄 인라인](#-인라인inline)
   - [📄 블록](#-블록block)
6. [📂 레이아웃](#-6-레이아웃)
   - [📄 레이아웃](#-레이아웃)

   
## 📂 1. How To
✔ CSS를 생성하는 법은 3가지가 있습니다.

###  📄 인라인 스타일

◽ 스타일 특성을 HTML 태그에 삽입  

◽ HTML 문서에 간단하게 CSS를 삽입할 수 있지만,  HTML 태그가 복잡해지는 단점

<details>
<summary>🔎예제 코드 확인</summary>

```JS
<html>
<head>
    <meta charset="utf-8">
    <title>인라인 스타일</title>
</head>
<body>
    <h3 style="color:#0fb382">제목입니다.</h3>
</body>
</html>
```

![image](https://user-images.githubusercontent.com/64937747/207759332-f0f846a4-41ad-48ed-9795-a1346ce87364.png)

</details>

<hr/>

### 📄 내부 스타일

◽ CSS 코드를 HTML 내부 \<style\> 태그에 삽입

<details>
<summary>🔎예제 코드 확인</summary>

```JS
<html>
<head>
    <meta charset="utf-8">
    <title>CSS 기본 구조 확인하기</title>
    <style>
        p {
            color: #31abcd;
            font-size: 20px;
        };

    </style>
</head>
<body>
    <p>나무의 줄기는 땅 위로 계속 높게 자라고 해마다굵기가 두꺼워지지만, 풀의 줄기는 일 년만 자라고 겨울을 나는 동안 땅 윗부분이 죽는다.</p>
</body>
</html>
```

![image](https://user-images.githubusercontent.com/64937747/207758745-786bd6e8-c164-40a8-b276-a5db9685f232.png)

</details>

<hr/>

### 📄 외부 스타일

◽ 외부에서 CSS 파일을 가져와 소스에 삽입

<details>
<summary>🔎예제 코드 확인</summary>

```JS
source : "mystyle.css"
  
h3 {
  color:rgb(29, 122, 91);
  font-size: 20px;
}
```

```JS
source : "external_style.html"
  
<html>
<head>
    <meta charset="utf-8">
    <title>외부 스타일 시트</title>
    <!-- css 가져오기 -->
    <link rel="stylesheet" type="text/css" href="mystyle.css">
</head>
<body>
    <h3>제목입니다.</h3>
</body>
</html>
```

![image](https://user-images.githubusercontent.com/64937747/207758375-15733f68-1e3e-4a1c-8e23-8ace778a1b33.png)

</details>

<hr/>

### 💡 CSS(Cascading Style Sheets)에서 캐스케이딩(Cascading)의 의미는?
> css의 스타일 속성들은 DOM 문서 트리에서 상위 앨리먼트에 있는 스타일 속성이 그 하위 앨리먼트로 흘려내려서 상속되기 때문입니다. (전부 상속된다는 소리는 아닙니다)  
> 
> 최상위 노드부터 아래로 스타일 속성들이 쭉 흘려내려(상속되어)가는 모습이 마치 폭포처럼 보이기 때문입니다.  
> 
> 폭포란게 무조건 다 흘러내려가는 것도 아니기 때문에 일부만 상속되는 것과 유사한 점 중 하나겠네요.

🔼[위로가기](#)

## 📂 2. 선택자
✔ CSS에서 스타일을 적용할 대상을 선택하기 위해 사용합니다.

###  📄 태그 선택자
◽ CSS를 적용할 대상으로 HTML 요소(태그)의 이름을 직접 사용할 수 있습니다.

<details>
<summary>🔎예제 코드 확인</summary>

```JS
<html>
<head>
    <meta charset="utf-8">
    <title>태그 선택자</title>
    <style>
        h2 {
            color:crimson;
            font-family: "맑은 고딕";
            font-size: 20px;
        }
        h3 {
            color:blue;
            font-size: 16px;
            font-style: italic;
            text-decoration: underline;
        }
        p {
            color: #444444;
            font-family: "돋움";
            font-size: 14px;
            line-height: 150%;
        }
    </style>
</head>
<body>
    <h2>향나무</h2> <!-- h2 태그 선택자 -->
    <h3>1. 특징</h3> <!-- h3 태그 선택자 -->
    <p>향나무는 높이가 20m까지 자란다. 새로 돋아나는 가지는 녹색이고 잎은 마주나거나 돌려나며 가지가 보이지 않을 정도로 밀생한다. 목재를 향으로 써왔기 때문에 향나무라고 한다.</p>
    <h3>2. 분포 및 종류</h3>
    <p>한국, 일본, 중국에 널리 분포하며, 예전에는 심산 지역, 특히 울릉도에서 많이 자랐으나 요즘은 관상용으로 많이 심는다. 침엽의 길이가 작고 비스드며 높는 것을 눈향나무, 지면으로 기어가듯 자라는 것을 섬향나무, 공처럼 둥근 수형이 되는 것을 둥근 향나무라고 부른다.</p> <!-- p 태그 선택자 -->
</body>
</html>
```
![image](https://user-images.githubusercontent.com/64937747/207805993-7b58a27b-052d-4756-b020-1592553fb60d.png)
</details>

<hr/>

### 📄 아이디 선택자
◽ 특정 아이디를 가지는 요소를 선택합니다.

<details>
<summary>🔎예제 코드 확인</summary>

```JS
<html>
<head>
    <meta charset="utf-8">
    <title>아이디 선택자</title>
    <style>
        p {
            color:#444444;
            line-height: 150%;
        }
        #position {
            color:burlywood;
            font-weight: bold;
        }
        #weather {
            color:blueviolet;
            font-weight: bold;
        }
        #kind {
            color:gold;
            font-style: italic;
            text-decoration: underline;
        }
    </style>
</head>
<body>
    <h3>다육식물이란?</h3>
    <p>다육식물은 <span id="position">사막</span>과 같이 수분이 적고 <span id="weather">건조한 기후</span>에서 살아남기 위해 줄기나 잎에 많은 수분을 저장하는 식물이다.</p>
    <p>다육식물은 일반적으로 <span id="kind">잎이 다육</span>이지만 줄기가 다육인 것도 있다.</p>
</body>
</html>
```
![image](https://user-images.githubusercontent.com/64937747/207808323-5bad9e54-b366-4739-9d6e-93ecd0ff1cd4.png)
</details>

<hr/>

### 📄 클래스 선택자
◽ 특정 집단을 클래스라 하며, 클래스 이름을 가지는 모든 요소를 선택합니다.

<details>
<summary>🔎예제 코드 확인</summary>

```JS
<html>
<head>
    <meta charset="utf-8">
    <title>클래스 선택자</title>
    <style>
        h1.orange {
            color: orange;
            font-size: 30px;
        }
        h2.orange {
            color: rgb(124, 86, 15);
        }
        p.blue {
            color: rgb(13, 137, 209);
            font-style: italic;
        }
        span.blue {
            color: rgb(18, 52, 204);
        }
        .blue {
            color: rgb(184, 19, 74);
        }
    </style>
</head>
<body>
    <h1 class="orange">제1회 봄빛 수목원 여름꽃 축제</h1>
    <h2 class="orange">수란, 수국, 무궁화, 원추리</h2>
    <p class="blue">아름다운 여름꽃과 시원한 바다를 경험할 수 있는 좋은 기회입니다.</p>
    <ul>
        <li>일자 : <span class="blue">6월 15일부터 8월 15일까지</span></li>
        <li>장소 : 봄빛 수목원 일원</li>
    </ul>
</body>
</html>
```

![image](https://user-images.githubusercontent.com/64937747/207894087-5769d146-43a4-4716-a41e-eeff4ed683af.png)

</details>

<hr/>

### 💡 선택자의 우선순위는 어떻게 될까요?
> 1. 속성 값 뒤에 !important를 붙인 속성
> 2. HTML에서 style을 직접 지정한 속성(인라인 스타일)
> 3. #id로 지정한 속성(아이디 선택자)
> 4. .클래스, :추상클래스로 지정한 속성(클래스 선택자)
> 5. 태그이름으로 지정한 속성(태그 선택자)
> 6. 상위 객체에 의해 상속된 속성
> > 🏆 우선순위 간단 정리
> >   
> > !important > 인라인 스타일 > 아이디 선택자 > 클래스 선택자> 태그 선택자


🔼[위로가기](#)

## 📂 3. 기본 속성
✔ CSS는 다양한 속성을 제공합니다.

### 📄 텍스트 속성

#### 📑 color

<details>
<summary>🔎 자세히</summary><br>

📌 텍스트의 색상을 설정합니다.  

📌 RGB 색상 코드로 색상을 지정합니다.

```JS
<html>
<head>
    <meta charset="utf-8">
    <title>color 속성</title>
    <style>
        h3 {
            color:bisque;
        }
        p {
            color:blueviolet;
        }
    </style>
</head>
<body>
    <h3>제비꽃</h3>
    <p>제비꽃은 우리나라 전역의 산과 들에 자라는 다년생 풀로써 물 빠짐이 좋은 양지 혹은 반음지에서 자란다. 가장자리에 얕고 둔한 톱니가 있고 긴 잎자루가 있는 잎이 모여나며, 보라색 또는 짙은 자색의 한 송이 꽃이 한쪽을 향해 핀다.</p>
</body>
</html>
```

![image](https://user-images.githubusercontent.com/64937747/207765713-95cc7e46-66bd-431e-b08f-a7fbbd4fa089.png)

</details>

#### 📑 text-align

<details>
<summary>🔎 자세히</summary><br>

📌 텍스트의 정렬 방향을 정합니다.  

📌 오른쪽, 왼쪽, 가운데 정렬, 양쪽 정렬이 있습니다.

```JS
<html>
<head>
    <meta charset="utf-8">
    <title>text-align</title>
    <style>
        h2 {
            text-align: center;
        }
    </style>
</head>
<body>
    <h2>로즈메리 허브</h2>
    <p>로즈메리는 남유럽이 원산지이며 1~2미터 까지 자라는 여러해살이품이다. 2~6월에 연보라색, 청자색, 연분홍, 흰색 꽃이 피며, 향기가 강해 꽃이나 잎을 조금만 건드려도 짙은 향기가 난다.</p>
</body>
</html>
```

![image](https://user-images.githubusercontent.com/64937747/207833501-db25d39e-fe30-41a6-b294-5acf3278819d.png)

</details>

#### 📑 text-decoration

<details>
<summary>🔎 자세히</summary><br>

📌 텍스트에 라인을 추가하여 꾸며줍니다.  

```JS
<html>
<head>
    <meta charset="utf-8">
    <title>text-decoration</title>
    <style>
        h2 {
            color: cadetblue;
            text-align: center;
            text-decoration: underline;
        }
    </style>
</head>
<body>
    <h2>로즈메리 허브</h2>
    <p>로즈메리는 남유럽이 원산지이며 1~2미터 까지 자라는 여러해살이품이다. 2~6월에 연보라색, 청자색, 연분홍, 흰색 꽃이 피며, 향기가 강해 꽃이나 잎을 조금만 건드려도 짙은 향기가 난다.</p>
</body>
</html>
```

![image](https://user-images.githubusercontent.com/64937747/207834811-19aa8774-bee3-4433-be41-4c49faa1ae9b.png)

</details>

#### 📑 line-height

<details>
<summary>🔎 자세히</summary><br>

📌 라인 높이를 정합니다.  

```JS
<html>
<head>
    <meta charset="utf-8">
    <title>line-height</title>
    <style>
        h2 {
            color: cadetblue;
            text-align: center;
            text-decoration: underline;
        }
        p {
            line-height: 200%;
        }
    </style>
</head>
<body>
    <h2>로즈메리 허브</h2>
    <p>로즈메리는 남유럽이 원산지이며 1~2미터 까지 자라는 여러해살이품이다. 2~6월에 연보라색, 청자색, 연분홍, 흰색 꽃이 피며, 향기가 강해 꽃이나 잎을 조금만 건드려도 짙은 향기가 난다.</p>
</body>
</html>
```

![image](https://user-images.githubusercontent.com/64937747/207835225-1a0a65f1-b5ed-4bc5-b40e-f5233b3c5af5.png)

</details>

#### 📑 text-shadow

<details>
<summary>🔎 자세히</summary><br>

📌 텍스트에 그림자를 추가합니다.

```JS
<html>
<head>
    <meta charset="utf-8">
    <title>글과 그림자</title>
    <style>
        h2 {
            color:cadetblue;
            text-shadow: 3px 3px 5px #444444;
        }
    </style>
</head>
<body>
    <h2>페퍼민트 허브</h2>
</body>
</html>
```
![image](https://user-images.githubusercontent.com/64937747/207766095-49fcfdf7-6522-4537-bc66-8cc71b59ffff.png)

</details>

<hr/>

### 📄 폰트 속성

#### 📑 font-family

<details>
<summary>🔎 자세히</summary><br>

📌 텍스트 폰트를 변경합니다.

```JS
<html>
<head>
    <meta charset="utf-8">
    <title>글자의 글꼴</title>
    <style>
        h2 {
            color:darkslateblue;
            font-family: "맑은 고딕";
        }
        p {
            color:goldenrod;
            font-family: "돋움";
        }
    </style>
</head>
<body>
    <h2>배롱나무</h2>
    <p>우리나라의 정원이나 공원 등에서 흔히 볼 수 있는 낙엽 활엽수로 높이는 5m 정도이다. 줄기는 연한 보랏빛을 띤 붉은빛이며 껍질이 벗겨져 있는 것을 자주 보게 되는데 벗겨진 자리는 희다. 꽃이 오랫동안 피기 때문에 목백일홍이라고도 부른다.</p>
</body>
</html>
```

![image](https://user-images.githubusercontent.com/64937747/207860022-3f1a311a-54e5-431d-8040-4f2c8ac18511.png)

</details>

#### 📑 font-style

<details>
<summary>🔎 자세히</summary><br>

📌 텍스트 폰트의 스타일을 변경합니다.

```JS
<html>
<head>
    <meta charset="utf-8">
    <title>글자의 스타일과 두께</title>
    <style>
        h1 {
            font-style: italic;
        }
        p {
            font-weight: bold;
        }
    </style>
</head>
<body>
    <h1>금계국</h1>
    <p>우리나라의 천변 제방이나 언덕에 많이 심겨 있는 한해살이풀또는 두해살이풀이다. 북아메리카가 원산지이며 관상용으로 화단에도 많이 재배한다.</p>
</body>
</html>
```
   
![image](https://user-images.githubusercontent.com/64937747/207860190-18ea8f82-8519-4916-8c90-787b798c6f75.png)

</details>

#### 📑 font-size

<details>
<summary>🔎 자세히</summary><br>

📌 텍스트 폰트의 크기를 변경합니다.

```JS
<html>
<head>
    <meta charset="utf-8">
    <title>글자의 크기</title>
    <style>
        h2 {
            font-family: "맑은 고딕";
            font-size: 20px;
        }
        p {
            font-family: "돋움";
            font-size: 14px;
        }
    </style>
</head>
<body>
    <h2>배롱나무</h2>
    <p>우리나라의 정원이나 공원 등에서 흔히 볼 수 있는 낙엽 활엽수로 높이는 5m 정도이다. 줄기는 연한 보랏빛을 띤 붉은빛이며 껍질이 벗겨져 있는 것을 자주 보게 되는데 벗겨진 자리는 희다. 꽃이 오랫동안 피기 때문에 목백일홍이라고도 부른다.</p>
</body>
</html>
```
![image](https://user-images.githubusercontent.com/64937747/207860428-bc7d7d84-fa6b-4254-82f0-6c5a63245dc9.png)
   
</details>

<hr/>

### 📄 링크 속성

#### 📑 a:link  

<details>
<summary>🔎 자세히</summary><br>

📌 방문하지 않은 링크

```JS
<html>
<head>
    <meta charset="utf-8">
    <title>방문하지 않은 링크</title>
    <style>
        a:link {
            color:black;
            text-decoration: none;
        }
    </style>
</head>
<body>
    <a href="#">자유게시판</a>
</body>
</html>
```
![image](https://user-images.githubusercontent.com/64937747/207829119-f379e571-b53a-40c4-a892-2fddf59105bf.png)

</details>

#### 📑 a:visited

<details>
<summary>🔎 자세히</summary><br>

📌 방문한 링크

```JS
<html>
<head>
    <meta charset="utf-8">
    <title>방문한 링크</title>
    <style>
        a:visited {
            color:cornflowerblue;
        }
    </style>
</head>
<body>
    <a href="#">자유게시판</a>
</body>
</html>
```
![image](https://user-images.githubusercontent.com/64937747/207829425-c594e75f-b372-4cb3-88fa-66772e0f66a9.png)

</details>

#### 📑 a:hover

<details>
<summary>🔎 자세히</summary><br>

📌 링크에 마우스를 올려놓을 때

```JS
<html>
<head>
    <meta charset="utf-8">
    <title>링크에 마우스를 올려놓을 때</title>
    <style>
        a:hover {
            color:darkorange;
            font-weight: bold;
            text-decoration: underline;
        }
    </style>
</head>
<body>
    <a href="#">자유게시판</a>
</body>
</html>
```
![image](https://user-images.githubusercontent.com/64937747/207829938-297730f0-d701-43c3-b0dc-64b649d502ce.png)

</details>

#### 📑 a:active

<details>
<summary>🔎 자세히</summary><br>

📌 링크를 클릭할 때

```JS
<html>
<head>
    <meta charset="utf-8">
    <title>링크를 클릭할 때</title>
    <style>
        a:active {
            color:rgb(141, 52, 141);
        }
    </style>
</head>
<body>
    <a href="#">자유게시판</a>
</body>
</html>
```
![image](https://user-images.githubusercontent.com/64937747/207830442-d336b4af-5b54-43fa-89e5-feb22ba0a9e8.png)

</details>

<hr/>

### 📄 배경 속성

#### 📑 background-color

<details>
<summary>🔎 자세히</summary><br>

📌 배경의 색상을 변경합니다.

```JS
<html>
<head>
    <meta charset="utf-8">
    <title>배경 색상</title>
    <style>
        body {
            background-color: bisque;
        }
        h1 {
            background-color:burlywood;
        }
        p {
            background-color: brown;
        }
        #cian {
            background-color: cadetblue;
        }
    </style>
</head>
<body>
    <h1>무궁화</h1>
    <p>무궁화는 우리나라 국화이며 <span id="cian">내한성의 낙엽관목</span>이다. 꽃은 흰색, 분홍색, 빨간색, 보라색 등 다양하고, 여러 가지 무늬의 화려한 꽃을 피운다. 꽃이 7월에서 10월까지 100일동안 피기 때문에 무궁화라는 이름이 붙었다.</p>
</body>
</html>
```
![image](https://user-images.githubusercontent.com/64937747/207895832-1ebf15d3-a3ab-4707-9800-2e28239ef8df.png)

</details>

#### 📑 background-image

<details>
<summary>🔎 자세히</summary><br>

📌 배경에 이미지를 추가합니다.

```JS
<html>
<head>
    <meta charset="utf-8">
    <title>배경 이미지</title>
    <style>
        body {
            background-image: url(https://user-images.githubusercontent.com/64937747/207814629-bd575956-e37d-4ba4-b4c2-cbfba77a0f64.jpg);
        }
    </style>
</head>
<body>
    <h1>무궁화</h1>
    <p><img src="https://user-images.githubusercontent.com/64937747/207814274-a84efd7d-62a1-444a-811c-f1cd74394034.jpg" alt=""></p>
</body>
</html>
```

![image](https://user-images.githubusercontent.com/64937747/207895995-cda9d1a7-b3a5-46b7-899c-d30dca24af4f.png)

</details>

#### 📑 background-repeat

<details>
<summary>🔎 자세히</summary><br>

📌 배경에 이미지를 반복해서 나타냅니다.  

📌 변화가 없는 이미지를 작은 크기로 잘라서 반복해 사용하면 용량이 작아져 로딩속도가 빨라집니다.

```JS
<html>
<head>
    <meta charset="utf-8">
    <title>배경 이미지</title>
    <style>
        body {
            background-image: url(https://user-images.githubusercontent.com/64937747/207816738-df1dd68c-5733-444b-acfd-6adc9e6548fa.png);
            background-repeat: repeat-x;
        }
    </style>
</head>
<body>
    <p><img src="https://user-images.githubusercontent.com/64937747/207816086-f2cf68db-dc4b-44fa-bc23-1a9c3363b9de.png" alt=""></p>
</body>
</html>
```

![image](https://user-images.githubusercontent.com/64937747/207896168-f7c6aed3-2f10-4d72-b6ba-4942ef6d05ee.png)

</details>

#### 📑 background-position

<details>
<summary>🔎 자세히</summary><br>

📌 배경에 이미지를 추가합니다.

```JS
<html>
<head>
    <meta charset="utf-8">
    <title>배경 위치</title>
    <style>
        body {
            background-image: url(https://user-images.githubusercontent.com/64937747/208026560-bbb309a9-ef57-4d7e-9d02-687b13f5b6bb.png);
            background-repeat: no-repeat;
            background-position: center top;
        }
        p {
            text-align: center;
        }
    </style>
</head>
<body>
    <br><br>
    <p><img src="https://user-images.githubusercontent.com/64937747/208026574-cd31ebf4-94c1-4c49-9aa5-84bccbb338d0.jpg" alt=""></p>
</body>
</html>
```

![image](https://user-images.githubusercontent.com/64937747/208026854-83f0c9e4-b6e5-41d3-a601-c864f98da303.png)

</details>

<hr/>

### 📄 목록 속성

#### 📑 list-style-type

<details>
<summary>🔎 자세히</summary><br>

📌 목록 앞에 붙는 도형이나 문자를 마커(Marker)라 부릅니다.  

📌 disc(default), circle(빈 동그라미), square(정사각형), none(표시하지 않음)

```JS
<html>
<head>
    <meta charset="utf-8">
    <style>
        li.square {
            list-style-type: square;
        }
        li.circle {
            list-style-type: circle;
        }
        li.dot {
            list-style-image: url(../img/dot_blue.gif);
        }
    </style>
</head>
<body>
    <h3>⭐ 녹색문화 체험여행</h3>
    <ul>
        <li class="square">숲 체험 : 수목원 탐방 + 숲 선생님과 생생 오감 활동</li>
        <li class="circle">곤충 체험 : 살아 있는 곤충 생태 관찰 + 체험 학습</li>
        <li class="dot">생태 체험 : 동물 먹이 주기 + 생태게임 + 자유 관람</li>
    </ul>
</body>
</html>
```

![image](https://user-images.githubusercontent.com/64937747/208026982-a2f5a3bc-7b7d-4393-83ac-f496817e6527.png)

</details>

#### 📑 list-style-image

<details>
<summary>🔎 자세히</summary><br>

📌 이미지를 이용해 마커(Maker)를 생성합니다.

```JS
<html>
<head><html>
<head>
    <meta charset="utf-8">
    <style>
        li {
            list-style-image: url(../img/dot_blue.gif);
        }
    </style>
</head>
<body>
    <h3>⭐ 녹색문화 체험여행</h3>
    <ul>
        <li id="square">숲 체험 : 수목원 탐방 + 숲 선생님과 생생 오감 활동</li>
        <li id="dot">곤충 체험 : 살아 있는 곤충 생태 관찰 + 체험 학습</li>
        <li>생태 체험 : 동물 먹이 주기 + 생태게임 + 자유 관람</li>
    </ul>
</body>
</html>
```

![image](https://user-images.githubusercontent.com/64937747/208027380-c7bc0499-8beb-4687-8f24-5fbdd9b5e040.png)

</details>

<hr/>

🔼[위로가기](#)

## 📂 4. 박스 모델
✔ 모든 HTML 요소는 박스(box)모양으로 구성되어 있으며, 이것을 박스 모델(box model)이라고 부릅니다.

✔ 박스 모델은 콘텐츠(content), 패딩(padding), 경계선(border), 마진(margin)으로 구분합니다.

### 💡 박스 모델을 시각적으로 나타내면 다음과 같습니다.
![box_model](https://user-images.githubusercontent.com/64937747/208029060-5ee13472-ef86-41cf-92e8-928e76fe5d2d.png)

### 📄 콘텐츠(content)

◽ 텍스트나 이미지가 들어있는 박스의 실질적인 내용입니다.

<details>
<summary>🔎예제 코드 확인</summary>

```JS
<html>
<head>
    <meta charset="utf-8">
    <style>
        p {
            width: 500px;
            border: solid 5px cadetblue;
        }
    </style>
</head>
<body>
    <p>
        봄빛 식물원은 2017년 12월 개원한 이래 방문한 고객들에게
        자연과 더불어 사는 즐거움을 선사하고 자연과의 만남을 통해
        삶의 여유와 행복을 제공하고 있습니다. ^^
    </p>
</body>
</html>
```

![image](https://user-images.githubusercontent.com/64937747/208054200-2f4cfc23-51ac-4002-95ac-9390d2741e09.png)

</details>

<hr/>

### 📄 패딩(padding)

◽ 콘텐츠와 테두리 사이의 간격입니다.

◽ 마진과 패딩의 여백을 설정하는 속성값은 개수만큼 구역 설정이 달라집니다.

◽ 패딩은 시각적으로 보이지 않습니다.

<details>
<summary>🔎예제 코드 확인</summary>

```JS
<html>
<head>
    <meta charset="utf-8">
    <style>
        p {
            width: 500px;
            border: dashed 5px cadetblue;
            padding: 10px 20px;
        }
    </style>
</head>
<body>
    <p>
        봄빛 식물원은 2017년 12월 개원한 이래 방문한 고객들에게
        자연과 더불어 사는 즐거움을 선사하고 자연과의 만남을 통해
        삶의 여유와 행복을 제공하고 있습니다. ^^
    </p>
</body>
</html>
```

![image](https://user-images.githubusercontent.com/64937747/208051617-6dee5744-77b7-43d4-a295-c80fac30ee23.png)

</details>

<hr/>

### 📄 테두리(border)

◽   콘텐츠와 패딩을 포함한 경계를 나타내는 선입니다

<details>
<summary>🔎예제 코드 확인</summary>

```JS
<html>
<head>
    <meta charset="utf-8">
    <style>
        p {
            width: 500px;
            border: dashed 5px cadetblue;
        }
    </style>
</head>
<body>
    <p>
        봄빛 식물원은 2017년 12월 개원한 이래 방문한 고객들에게
        자연과 더불어 사는 즐거움을 선사하고 자연과의 만남을 통해
        삶의 여유와 행복을 제공하고 있습니다. ^^
    </p>
</body>
</html>
```

![image](https://user-images.githubusercontent.com/64937747/208055328-188cb67c-bc46-43b7-ba08-ffe12eeef86f.png)

</details>

<hr/>

### 📄 마진(margin)

◽ 테두리와 이웃하는 요소 사이의 간격입니다.  

◽ 마진은 시각적으로 보이지 않습니다.

<details>
<summary>🔎예제 코드 확인</summary>

```JS
<html>
<head>
    <meta charset="utf-8">
    <style>
        p {
            width: 500px;
            border: dashed 5px cadetblue;
            padding: 50px 30px;
            margin: 30px 50px 30px 50px;
        }
    </style>
</head>
<body>
    <p>
        봄빛 식물원은 2017년 12월 개원한 이래 방문한 고객들에게
        자연과 더불어 사는 즐거움을 선사하고 자연과의 만남을 통해
        삶의 여유와 행복을 제공하고 있습니다. ^^
    </p>
</body>
</html>
```

![image](https://user-images.githubusercontent.com/64937747/208055439-36cadd67-01d8-418a-b7f6-a3843a887b8c.png)

</details>

<hr/>

🔼[위로가기](#)

## 📂 5. 디스플레이
✔ 웹 페이지의 레이아웃(layout)을 결정하는 CSS의 속성입니다.  

✔ 해당 HTML 요소가 웹 브라우저에 어떻게 보이는가를 결정합니다.

### 📄 인라인(inline)

◽ HTML 요소의 크기를 설정할 수 없으며 수평 방향으로 디스플레이됩니다.  

◽ 대표적으로 \<span>, \<a>, \<img> 등이 있습니다.

<details>
<summary>🔎예제 코드 확인</summary>

```JS
<html>
<head>
    <meta charset="utf-8">
    <title>inline</title>
    <style>
        * {
            margin: 0;
            padding: 0;
        }
        ul {
            list-style-type: none;
        }
        #menu {
            width: 500px;
            padding: 10px;
            margin: 20px 0 0 40px;
            background-color: #eeeeee;
            border: solid 1px aaaaaa;
            display: inline;
            text-align: center;
        }
        #menu li {
            display: inline;
        }
    </style>
</head>
<body>
    <ul id="menu">
        <li>회사소개 |</li>
        <li>제품소개 |</li>
        <li>공지사항 |</li>
        <li>업무제휴 |</li>
        <li>고객센터</li>
    </ul>
</body>
</html>
```

![image](https://user-images.githubusercontent.com/64937747/208055768-7a5d83ca-5cc4-4ba2-963d-7b038236906e.png)

</details>

<hr/>

### 📄 블록(block)

◽ HTML 요소의 크기를 설정할 수 있으며 줄에 하나씩 수직 방향으로 디스플레이됩니다.  

◽ 대표적으로 \<div>, \<h1>, \<p>, \<ul>, \<ol>, \<form> 등이 있습니다.

<details>
<summary>🔎예제 코드 확인</summary>

```JS
<html>
<head>
    <meta charset="utf-8">
    <title>block</title>
    <style>
        a {
            display: block;
        }
    </style>
</head>
<body>
    <p>수직 방향 메뉴</p>
    <a href="http://naver.com" target="_blank">네이버</a>
    <a href="http://daum.net" target="_blank">다음</a>
    <a href="http://google.com" target="_blank">구글</a>
</body>
</html>
```

![image](https://user-images.githubusercontent.com/64937747/208056049-63b72a86-fb54-4e59-80d6-b1c240d6ab82.png)

</details>

<hr/>

### 💡 일반적인 웹페이지 레이아웃

![website_layout](https://user-images.githubusercontent.com/64937747/208061014-0ef0e924-d1ca-4167-b827-b140a2baf8db.png)

🔼[위로가기](#)