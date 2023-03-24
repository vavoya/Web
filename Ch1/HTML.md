# DOM
## DOM은 정확히 무엇일까?
DOM(Document Object Model)은 웹 페이지에 대한 인터페이스. 기본적으로 여러 프로그램들이 페이지의 콘텐츠 및 구조, 그리고 스타일을 읽고 조작할 수 있도록 API를 제공.

## 웹 페이지는 어떻게 만들어질까?
웹 브라우저가 원본 HTML 문서를 읽음 -> 스타일을 입히고 대화형 페이지로 만들어 뷰 포트에 표히하기 까지의 과정을 "Critical Rendering Path"라고 한다. Understanding the Critical Rendering Path 에서 다루듯이 이 과정은 여러 단계로 나누어져 있지만, 이 단계들은 대략 두 단계로 나눌 수 있다. 
첫 번째 단계에서 브라우저는 읽어들인 문서를 파싱(parsing 구문 분석)하여 최종적으로 어떤 내용을 페이지에 렌더링할지 결정.
두 번째 단계에서 브라우저는 해당 렌더링을 수행.
<img src="https://wit.nts-corp.com/wp-content/uploads/2019/02/-1">
첫 번째 과정을 거치면 "렌더 트리"가 생성된다.
렌더 트리는 웹 페이지에 표시될 HTML 요소들과 이와 관련된 스타일 요소들로 구성. 브라우저는 렌더 트리를 생성하기 위해 다음과 같이 두 모델이 필요
- DOM(Document Object Model) - HTML 요소들의 구조화된 표현
- CSSOM(Cascading Style Sheets Object Model) - 요소들과 연관된 스타일 정보의 구조화된 표현

## DOM은 어떻게 생성될까 (그리고 어떻게 보여질까)?
DOM은 원본 HTML 문서의 객체 기반 표현 방식. 둘은 서로 비슷하지만, DOM이 갖고 있는 근본적인 차이는 단순 텍스트로 구성된 HTML 문서의 내용과 구조가 객체 모델로 변환되어 다양한 프로그램에서 사용될 수 있다는 점.
DOM의 객체 구조는 "노드 트리"로 표현된다. 하나의 부모 줄기가 여러 개의 자식 나뭇가지를 갖고 있고, 또 각각의 나뭇가지는 잎들을 가질 수 있는 나무와 같은 구조로 이루어져 있기 떄문이다. 이 케이스의 경우, 루트 요소인 \<html\>은 "부모 줄기", 루트 요소에 내표된 태그들은 "자식 나뭇가지" 그리고 요소 안의 컨텐츠는 "잎"에 해당한다.
아래 HTML 예시에서,
``` html
<!doctype html>
<html lang="en">
	<head>
		<title>My first web page</title>
	</head>
	<body>
		<h1>Hello, world!</h1>
		<p>How are you?</p>
	</body>
</html>
```
이 문서는 아래와 같은 노드 트리로 표현된다.
<img src="https://wit.nts-corp.com/wp-content/uploads/2019/02/-3">

## DOM이 아닌 것
위 예제 혹은 DevTools에서 DOM은 마치 HTML 문서와 1대1 매핑이 되는 것 처럼 보인다. 그러나 둘 간에는 몇 가지 차이점이 있다.

### 1. DOM은 HTML이 아니다.
DOM은 HTML 문서로부터 생성되지만 항상 동일하지 않습니다. DOM이 원본 HTML 소스와 다를 수 있는 두가지 케이스가 있습니다.

#### 작성된 HTML 문서가 유효하지 않을 때
DOM은 유효한 HTML 문서의 인터페이스 이다. DOM을 생성하는 동안, 브라우저는 유효하지 않는 HTML 코드를 올바르게 교정한다.
아래 예시를 살펴보면,
```html
<!doctype html>
<html>
Hello, world!
</html>
```
문서에 유효한 HTML 규칙의 필수 사항인 \<head\> 와 \<body\> 요소가 빠져있다. 그렇지만 생성된 DOM 트리에는 올바르게 교정되어 나타난다.
<img src="https://wit.nts-corp.com/wp-content/uploads/2019/02/-5">

#### 자바스크립트에 의해 DOM이 수정될 때
DOM은 HTML 문서의 내용을 볼 수 있는 인터페이스 역할을 하는 동시에 동적 자원이 되어 수정될 수 있다.
예를 들어, 자바스크립트를 사용해 DOM에 새로운 노드를 추가할 수 있다.
```JS
var newParagraph = document.createElement("p");
var paragraphContent = document.createTextNode("I'm new!");
newParagraph.appendChild(paragraphContetn);
document.body.appendChild(newParagraph);
```
이 코드는 DOM을 업데이트 한다. 하지만 HTML 문서의 내용을 변경하지 않는다.

### 2. DOM은 브라우저에서 보이는 것이 아니다.
브라우저 뷰 포트에 보이는 것은 렌더 트리로 DOM과 CSSOM의 조합이다. 렌더 트리는 오직 스크린에 그려지는 것으로 구성되어 있어 DOM과 다르다.
달리 말하면, 렌더링 되는 요소만이 관련 있기 때문에 시각적으로 보이지 않는 요소는 제외된다.
예를 들어, ***display: none*** 스타일 속성을 가지고 있는 요소이다.
```html
<html lang="en">
	<head></head>
	<body>
		<h1>Hello, world!</h1>
		<p style="dispaly : none;">How are you?</p>
	</body>
</html>
```
DOM은 \<p\>요소를 포함시킨다.
<img src="
https://wit.nts-corp.com/wp-content/uploads/2019/02/-9">
그러나 렌더 트리에 해당하는 뷰 포트에 표시되는 내용은 \<p\>요소를 포함하지 않는다.
<img src="https://wit.nts-corp.com/wp-content/uploads/2019/02/-8">

### 3. DOM은 개발도구에서 보이는 것이 아니다.
개발도구의 요소 검사기는 DOM과 가장 가까운 근사치를 제공한다. 그러나 개발도구의 요소 검사기는 DOM에 없는 추가적인 정보를 포함한다.
가장 좋은 예는 CSS의 가상 요소이다. ***::before*** 과 ***::after*** 선택자를 사용하여 생성된 가상 요소는 CSSOM과 렌더 트리의 일부를 구성한다.
하지만, 기술적으로 DOM의 일부는 아니다. DOM은 오직 원본 HTML 문서로부터 빌드 되고, 요소에 적용되는 스타일을 포함하지 않기 때문이다.
가상 요소가 DOM의 일부가 아님에도 불구하고, 요소 검사기에서는 아래와 같이 확인된다.
<img src="https://wit.nts-corp.com/wp-content/uploads/2019/02/-10">
이러한 이유로 가상 요소는 DOM의 일부가 아니기 때문에 자바스크립트에 의해 수정될 수 없다.

## 요약정리
DOM은 HTML 문서에 대한 인터페이스이다. 첫째로 뷰 포트에 무엇을 렌더링 할지 결정하기 위해 사용되며,
둘째로는 페이지의 콘텐츠 및 구조, 그리고 스타일이 자바스크립트 프로그램에 의해 수정되기 위해 사용된다.
DOM은 원본 HTML 문서 형태와 비슷하지만 몇가지 차이점이 있다.
- 항상 유효한 HTML 형식이다.
- 자바스크립트에 수정될 수 있는 동적 모델이어야 한다.
- 가상 요소를 포함하지 않는다. (EX. ***:after***)
- 보이지 않는 요소를 포함한다. (EX. ***:display: none***)


# \<div\> 태그
HTML 문서에서 특정 영역(division)이나 구획(section)을 정의할 때 사용

\<div\> 요소는 여러 HTML 요소들을 하나로 묶어주어 CSS로 스타일을 변경하거나 자바스크립트로 특정 작업을 수행하기 위한 일종의 컨테이너(container)로 자주 사용됩니다. 또한, CSS와 함께 웹 페이지의 레이아웃(layout)을 설정하는데도 종종 사용됩니다.

```css
<style>
	div {
		background-color: orange;
		font-style: italic;
	}
</style>

<p>HTML의 모든 요소는 해당 요소가 웹 브라우저에 어떻게 보이는가를 결정짓는 display 속성을 가진다.</p>
<div><p>div 요소는 다른 HTML 요소들을 하나로 묶는 데 자주 사용되는 대표적인 블록(block) 요소입니다.</p></div>
<p>span 요소는 텍스트(text)의 특정 부분을 묶는 데 자주 사용되는 인라인(inline) 요소입니다.</p>
```
이외에도 .class로 묶을 수 도 있다.
```css
<head>
  <style>
    .my-class {
      background-color: orange;
      font-style: italic;
    }
  </style>
</head>
<body>
  <div class="my-class">Hello World</div>
  <div>Hello World</div>
  <div class="my-class">Hello World</div>
</body>

```


# <img> \<img\>태그
**: 이미지 삽입**
```html
<img src="이미지 경로">
```
웹 페이지에 이미지를 넣을 때 사용한다. \<img\> 태그 하나당 1개의 이미지를 삽입할 수 있다.
inline태그(앞뒤로 줄 바꿈 X), 반드시 src속성(source)을 사용해서 이미지의 경로를 지정해야한다.
```html
<img src="파일경로" alt="설명" width="500" height="600">
<img src="웹 페이지 이미지 주소">
```

## img의 속성
| attribute | Description                           |
| --------- | ------------------------------------- |
| width     | 너비                                  |
| height    | 높이                                  |
| alt       | 이미지를 설명해 주는 대체 텍스트 추가 |
| title     | 툴팁(커서 올렸을 때 설명 나오는 것    |
| usemap    | 이미지 맵(하나의 이미지에 여러개의 링크를 만드는 것)                                      |


# \<input\> 태그
**: 입력 필드**
\<input\>요소는 사용자가 데이터를 입력할 수 있는 입력 필드를 선언하기 위해 \<form\> 요소 내부에서 사용됩니다.
이러한 입력 필드는 \<input\> 요소와 type 속성값을 달리함으로써 여러 가지 모양으로 나타낼 수 있습니다.
```html
<form action="/example/media/action_target.php" method="get">
	이름 : <input type="text" name="st_name"><br>
	학번 : <input type="text" name="st_id"><br>
	학과 : <input type="text" name="department"><br>
	<input type="submit">
</form>
```
<form action="/example/media/action_target.php" method="get">
	이름 : <input type="text" name="st_name"><br>
	학번 : <input type="text" name="st_id"><br>
	학과 : <input type="text" name="department"><br>
	<input type="submit">
</form>
\<input\> 요소는 빈 태그(empty tag)이며, 속성만을 포함하고 있습니다.
\<label\> 요소를 사용하면 \<input\> 요소의 라벨(label)을 정의할 수 도 있습니다.


# \<a\> 태그
**: anchor, 웹 페이지나 외부 사이트 연결**
```html
<a href="연결할 링크의 경로"> 내용 </a>
```
링크로 사용할 텍스트나 이미지를 \<a\>로 묶고 href(hypertext reference)속성을 이용해서 연결할 웹 페이지의 이름이나 웹 사이트 주소를 지정하면 된다.
<a href="https://www.google.com"> 구글로 이동 </a>
==href="#"은 실제로 연결되지 않는, 링크 역할만 하도록 만든 것, 널 링크(null link)라고 한다.==

## \<a\>에서 사용할 수 있는 속성 값
1) **href** : href 어트리뷰트는 이동하고자 하는 파일의 위치(경로)를 값으로 받는다. 경로(path)란 파일 시스템 상에서 특정 파일의 위치를 의미한다
| Value               | Description                                                    |
| ------------------- | -------------------------------------------------------------- |
| 절대 URL            | 웹 사이트 URL (href="https://www.example.com/default.html")    |
| 상대 URL            | 자신의 위치를 기준으로한 대상의 URL (href="html/default.html") |
| fragment identifier | 페이지 내의 특정 id를 갖는 요소에의 링크 (href="#top")         |
| 메일                | mailto:|
| script              | href="javascript:alert('Hello');"|
```html
<a href="http://www.google.com">URL</a><br>
<a href="html/my.html">Local file</a><br>
<a href="file/my.pdf" download>Download file</a><br>
<a href="#">fragment identifier</a><br>
<a href="mailto:someone@example.com?Subject=Hello again">Send Mail</a><br>
<a href="javascript:alert('Hello');">Javascript</a>

<h2 id="top">Top of page!</h2>
<a href="#top">Go to top</a>
```

2) **target** : 새 창 or 새 탭에서 링크를 열 때 사용
| \_blank  | 새로운 탭 or 창                                        |
| -------- | ------------------------------------------------------ |
| \_self   | 현재 탭 or 창                                          |
| \_parent | 현재 화면을 불러낸 부모 탭 or 창, 없으면 현재 탭 or 창 |
| \_top    | 최상위 탭 or 창, 없으면 현재 탭 or 창|

3) **title** : 링크의 툴팁을 표시(커서를 올렸을 때 나오는 설명)
```html
<a href="연결할 페이지나 사이트 경로" title="링크 내용에 대한 설명"
```

4) **id** : 같은 페이지 안에서 이동할 때 사용
이동하고 싶은 위치마다 id 속성을 이용하여 앵커를 만든다(각각 다른 이름으로 지정해야함)
```html
<p id="앵커이름">내용</p>
```
이름 붙여높은 앵커들은 다시 \<a\> 의 href 속성으로 연결
```html
<a href="#앵커이름">내용</a>
```
해당 링크를 누르게 되면 id 지정해놓은 p태그 문단으로 화면이 이동되게 된다.

## download속성
HTML5에 추가된 속성 중 \<a\> 태그에만 추가된 download라는 속성이 있다.
브라우저는 \<a\> 태그에 download 속성이 설정되어 있으면 링크가 가리키는 파일을 다운로드한다.
즉, 마치 링크 위에서 마우스 오른쪽 버튼을 클릭하고 "다른 이름으로 링크 저장"을 실행하는 것과 같다.
```html
<a href="원하는_주소" download>download 속성 예제</a>
```
download 속성에는 파일 이름으로 사용할 문자열을 입력할 수 도 있다.
```js
const $downloadButton = document.querySelector('.download-button');

$downloadButton.href = // 다운로드 링크 지정
$downloadBUtton.download = `recordinf_${new Date().toDateString()}.webm`;
```


# \<span\> 태그
\<div\> 태그처럼 특별한 기능을 갖고있지 않고, CSS와 함께 쓰인다.

\<div\> 태그와의 차이점은 display 속성이 block이 아닌, inline 이라는 점인데, 이는 CSS display 항목에서 세부 정보를 알 수 있다.
이 둘의 차이를 쉽게 설명하자면, \<div\>는 줄 바꿈이 되지만, \<span\>은 줄 바꿈이 되지 않는다.
```html
<html>
<body>
	<span style="background-color:red">span1</span>
	<span style="background-color:blue">span2</span>
	<span style="background-color:green">span3</span>
</body>
</html>
```


# id, class
태그에서 설정한 id 나 class 속성에 따라 스타일을 지정
```html
<html>
<head>
<style>
	#m_box{ background-color: #09C; width: 150px; height: 40px; }
	.box{ width: 100px; height: 50px; border: 1px solid green }
</style>
</head>
<body>
	<div class="box">box 클래스</div>
	<div class="box">box 클래스</div>
	<div id="m_box">m_box 아이디</div>
</body>
</html>
```


# Markup Language
- 태그 등을 이용하여 문서나 데이터의 구조를 명기하는 언어의 한 가지
- 태그
	- 원래 텍스트와는 별도로 원고의 교정부호 및 주석을 표현하기 위한 것이었으나 용도가 점차 확장되어 문서의 구조를 표현하는 역할을 하게 됨
	- 문서의 골격에 해당하는 부분을 작성
- 일반적으로는 데이터를 기술하는 정도로만 사용되기 때문에 프로그래밍 언어와는 구분됨


# Reference
https://wit.nts-corp.com/2019/02/14/5522
https://inpa.tistory.com/entry/HTML-🏷%EF%B8%8F-태그-요약표#태그%3C/%3E_모음_요약표
https://ofcourse.kr/html-course/span-태그
https://ofcourse.kr/css-course/부모-자식-선택자
https://gptjs409.github.io/infra/2019/09/08/markup-language.html
