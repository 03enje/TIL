# HTML 태그
> HTML에서 사용하는 명령어

## 📃목차
- [HTML 태그](#HTML-)
  + [1. 텍스트 태그](#1-텍스트-태그)
  + [2. 목록 태그](#2-목록-태그)  
  + [3. 링크 태그](#3-링크-태그)  
  + [4. 이미지 태그](#4-이미지-태그)  
  + [5. 오디오 태그](#5-오디오-태그)  
  + [6. 비디오 태그](#6-비디오-태그)  
  + [7. 테이블 태그](#7-테이블-태그)  
 
## 1. 텍스트 태그
### 제목 태그

> 제목을 표현하기 위해 사용하는 태그 : \<h1\> ~ \<h6\>
> > h의 의미는 'heading'

<details>
<summary>🔎예제 코드 확인</summary>

```JS
<html>
<head>
    <meta charset="utf-8">
    <title>제목 연습(h1~h6)</title>
</head>
<body>
    <h1>글자 제목(h1)</h1>
    <h2>글자 제목(h2)</h2>
    <h3>글자 제목(h3)</h3>
    <h4>글자 제목(h4)</h4>
    <h5>글자 제목(h5)</h5>
    <h6>글자 제목(h6)</h6>
</body>
</html>
```
![image](https://user-images.githubusercontent.com/64937747/207502035-89b9c341-1387-42d4-b2e6-6e22cf26f755.png)

🔼[돌아가기](#목차)
</details>

<hr/>

### 줄바꿈 태그

> 줄바꿈을 하기 위한 태그 : \<br\>
> > br의 의미는 'line break'

<details>
<summary>🔎예제 코드 확인</summary>

* 줄바꿈 태그가 없는 경우
```JS
<html>
<head>
    <meta charset="utf-8">
    <title>줄바꿈 태그가 없는 경우</title>
</head>
<body>
안녕하세요.



반갑습니다.
열심히 HTML를 공부해 보아요
</body>
</html>
```
![image](https://user-images.githubusercontent.com/64937747/207504264-c6f585f1-52be-48f3-9cee-b927c98af2db.png)

* 줄바꿈 태그가 있는 경우
```JS
<html>
<head>
    <meta charset="utf-8">
    <title>줄바꿈 태그가 있는 경우</title>
</head>
<body>
안녕하세요.
<br>
<br>
<br>
반갑습니다.<br>
열심히 HTML를 공부해 보아요
</body>
</html>
```
![image](https://user-images.githubusercontent.com/64937747/207541129-05e40180-a8c3-45be-b9fc-28b065a1d650.png)

🔼[돌아가기](#목차)
</details>

<hr/>

### 단락 태그
> 단락을 나누는 태그 : \<p\>
> > p의 의미는 'paragraph'

<details>
<summary>🔎예제 코드 확인</summary>

```JS
<html>
<head>
    <meta charset="utf-8">
    <title>단락 연습</title>
</head>
<body>
    <h3>튤립</h3>
    <p>튤립은 여러 종류의 품종으로 나누어져 있어 각기 아름다운 꽃을 감상할 수 있습니다.</p>
    <p>햇볓이 잘 들고 배수가 잘되는 토양에 심는 것이 적합합니다.</p>
</body>
</html>
```
![image](https://user-images.githubusercontent.com/64937747/207511704-8344b4c8-c608-4e74-8577-7e5270e4cddf.png)

🔼[돌아가기](#목차)
</details>

<hr/>

### 💡 특수 문자 표현

|표현|기능|내용|
|---|---|---|
|\&nbsp;|공백 표현|&nbsp;|
|\&lt;|왼쪽 꺾쇠 괄호 표현|&lt;|
|\&gt;|오른쪽 꺾쇠 괄호 표현|&gt;|
|\&amp;|앰퍼샌드 표현|&amp;|
|\&quot;|쌍따옴표 표현|&quot;|
|\&copy;|카피 표현|&copy;|

## 2. 목록 태그
### 2.1 비순서 태그
> 정렬 순서와 상관없이 나타내는 태그 : \<ul\>, \<li\>
> > ul의 의미는 'unordered list', li의 의미는 'list item'

<details>
<summary>🔎예제 코드 확인</summary>

```JS
<html>
<head>
    <meta charset="utf-8">
    <title>순서 없는 목록</title>
</head>
<body>
    <h2>식물원 관람 유의사항</h2>
    <ul>
        <li>입장권에 게시된 관람요령을 살펴보시기 바랍니다.</li>
        <li>안내원의 안내에 따라주시기 바랍니다.</li>
        <li>관람 지역 이외의 출입제한 지역은 출입을 금합니다.</li>
        <li>식물이 식재된 곳에 들어가지 마십시오.</li>
    </ul>
</body>
</html>
```
![image](https://user-images.githubusercontent.com/64937747/207544883-551c71cf-42ae-4f86-8353-0260fee31503.png)

🔼[돌아가기](#목차)
</details>

<hr/>

### 2.2 순서 태그
> 정렬 순서대로 나타내는 태그 : \<ol\>, \<li\>
> > ul의 의미는 'ordered list', li의 의미는 'list item'

<details>
<summary>🔎예제 코드 확인</summary>

```JS
<html>
<head>
    <meta charset="utf-8">
    <title>순서 있는 목록 나타내기</title>
</head>
<body>
    <h3>가족 생태체험여행</h3>
    <ol>
        <li>기간: 2022년 05월 ~ 10월</li>
        <li>대상: 가족(초등학생 이상 어린이, 부모 및 동반자 참여)<br>
            ※ 프로그램의 성격에 따라 대상자의 연령이 변경될 수 있습니다.</li>
        <li>인원: 1반 20명 내외(부모 포함)</li>
        <li>참가비: 해당 프로그램 참조</li>
        <li>신청방법: 홈페이지 신청, 사전결제(카드)</li>
    </ol>
</body>
</html>
```
![image](https://user-images.githubusercontent.com/64937747/207545004-0c443270-ed4c-428f-a537-6a203a034b0c.png)

🔼[돌아가기](#목차)
</details>

<hr/>

## 3. 링크 태그
### 3.1 앵커 태그
> 하이퍼링크를 생성하기 위한 태그 : \<a\>, 속성 : href ...
> > a의 의미는 'anchor', href의 의미는 'hypertext reference'  
> >    
> > 하이퍼링크란, 하이퍼텍스트 문서 안에서 직접 모든 형식의 자료(동영상, 사진, 글 등)를 연결하고 가리킬 수 있는 참조 링크(link)를 의미

<details>
<summary>🔎예제 코드 확인</summary>

```JS
source : "index.html"

<html>
<head>
    <meta charset="utf-8">
    <title>링크 연습</title>
</head>
<body>
    <a href="page1.html">꽃잔디 링크</a><br><br>
    <a href="page2.html">옥잠화 링크</a><br><br>
    <a href="page3.html">맥문동 링크</a><br><br>
</body>
</html>
```
![image](https://user-images.githubusercontent.com/64937747/207523347-17bad6cb-7202-45a8-bb16-9736176aaab5.png)

```JS
source : "page1.html"

<html>
<head>
    <meta charset="utf-8">
    <title>꽃잔디 링크(page1)</title>
</head>
<body>
    <h3>꽃잔디</h3>
    <img src="../img/ground_pink.jpg" width="300"><br>
    <p>꽃잔디는 아메리카 동부가 원산지로 원래는 건조한 모래땅에서 자라는 여러해살이풀이며 높이 10CM까지 자란다. 잎은 마주나기이며, 가장자리가 밋밋하고 털이 있다. 붉은색, 자홍색, 분홍색, 흰색 등 다양한 색깔의 꽃이 핀다.</p>
    <a href="index.html"><u><b>홈으로</b></u></a>
</body>
</html>
```
![image](https://user-images.githubusercontent.com/64937747/207523444-cfe42ee3-fe33-4ec9-9120-6a5e2bd508ac.png)

🔼[돌아가기](#목차)
</details>

<hr/>

## 4. 이미지 태그
> 이미지를 생성하기 위한 태그 : \<img\>, 속성 : src, alt ...
> > img의 의미는 'image', src의 의미는 'source', alt의 의미는 'alternative'  
> >     
> > src는 포함하고자 하는 파일의 경로를 지정, alt는 이미지의 대체 텍스트이며 네트워크 오류 등 이미지를 표시할 수 없는 경우 이 속성 값을 대신 표시

<details>
<summary>🔎예제 코드 확인</summary>

```JS
<html>
<head>
    <meta charset="utf-8">
    <title>야생화</title>
</head>
<body>
    <h3>금계국</h3>
    <img src="../img/flower.jpg" alt="금계국 이미지"><br>
    <p>금계국은 북아메리카 원산이며 관상용으로 화단에서 재배한다.
        6월에서 8월에 지름 2.5cm에서 5cm 사이의 노란꽃이 줄기와 가지 끝에 한 송이씩 핀다. 
        물 빠짐이 좋은 모래흙이나 마사토에서 잘 자란다.</p>
</body>
</html>
```
![image](https://user-images.githubusercontent.com/64937747/207526080-beccc302-af2a-456b-9ba6-4952b759c1a9.png)

🔼[돌아가기](#목차)
</details>

## 5. 오디오 태그
> 오디오를 생성하기 위한 태그 : \<audio\>, 속성 : autoplay, controls ...
> > autoplay는 오디오를 사이트에서 자동으로 재생, controls는 컨트롤러를 브라우저에서 제공

<details>
<summary>🔎예제 코드 확인</summary>

```JS
<html>
<head>
    <meta charset="utf-8">
    <title></title>
</head>
<body>
    <audio src="evocation.mp3" autoplay controls></audio>
</body>
</html>
```
![image](https://user-images.githubusercontent.com/64937747/207530104-b9e4c631-dac3-40de-b5be-184ce6f80ee6.png)

🔼[돌아가기](#목차)
</details>


## 6. 비디오 태그
> 비디오를 생성하기 위한 태그 : \<video\>, 속성 : loop, width, height ...
> > loop는 영상을 무한 재생, width는 영상의 너비를 지정, height는 영상의 높이를 지정

<details>
<summary>🔎예제 코드 확인</summary>

```JS
<html>
<head>
    <meta charset="utf-8">
    <title>비디오 삽입</title>
</head>
<body>
    <h3>비디오</h3>
    <hr>
    <video src="movie.mp4" width="320" height="121" controls autoplay></video>
</body>
</html>
```
![image](https://user-images.githubusercontent.com/64937747/207530836-d8ba318a-f0ae-4a8d-964d-8809f304b19b.png)

🔼[돌아가기](#목차)
</details>

## 7. 테이블 태그
> 테이블을 생성하기 위한 태그 : \<table\>, \<tr\>, \<td\>, 속성 : rowspan, colspan ...
> > \<tr\>은 행(table row)을 나타내는 태그, \<td\>은 열(table data)을 나타내는 태그
> >
> > rowspan은 행을 병합, colspan은 열을 병합

<details>
<summary>🔎예제 코드 확인</summary>

```JS
<html>
<head>
    <meta charset="utf-8">
    <!-- 선택자 -->
    <style>
        table, th, tr, td {
            border: solid 1px black; 
            border-collapse: collapse;
            padding: 8px;
        }
    </style>
</head>
<body>
    <table>
        <tr>
            <th>지역</th>
            <th>현재기온</th>
            <th colspan="2">불쾌지수/습도(%)</th>
            <th>풍속(m/s)</th>
        </tr>
        <tr>
            <td rowspan="2">서울/경기</td>
            <td>23</td>
            <td>60</td>
            <td>80</td>
            <td>4.7</td>
        </tr>
        <tr>
            <td>29</td>
            <td>60</td>
            <td>80</td>
            <td>5.0</td>
        </tr>
        <tr>
            <td>제주도</td>
            <td>21</td>
            <td>65</td>
            <td>85</td>
            <td>3.6</td>
        </tr>
    </table>
</body>
</html>
```
![image](https://user-images.githubusercontent.com/64937747/207557182-eb0e6fca-27cf-4cc3-9f04-99ec3ab0bd00.png)

🔼[돌아가기](#목차)
</details>
