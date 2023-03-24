# 선택자
CSS의 선택자는 HTML 문서에서 스타일을 적용하려는 대상을 선택하는 방법
다음과 같은 선택자 유형이 있다.
1. **태그 선택자** : HTML 요소에 태그 이름을 사용하여 스타일을 적용한다. 예를 들어, \<div\> 선택자는 모든 \<div\> 요소에 스타일으 적용한다.
2. **ID 선택자** : HTML 요소의 ID 속성 값을 사용하여 스타일을 적용한다. 예를 들어, "#my-id" 선택자는 id 속성 값이 "my-id"인 요소에 스타일을 적용한다.
3. **클래스 선택자** : HTML 요소의 class 속성 값을 사용하여 스타일을 적용한다. 예를 들어, ".my-class" 선택자는 class 속성 값이 "my-class"인 모든 요소에 스타일을 적용한다.
4. **그 외 선택자** : 속성 선택자, 자식 선택자, 후손 선택자 등 다양한 선택자 유형이 있다. 이러한 선택자는 특정 상황에 맞게 사용된다.

## 용어
- **CSS 규칙 선언(declaration block)** : 선택자(selector)와 중괄호로 이루어져 있으며, 중괄호 안에는 스타일 속성(property)과 값(value)이 쌍을 이루어 적용된다.
``` css
h1 { font-size: 2em; color: blue; }
```
- **CSS 스타일링** 
```html
<h1>Welcome to CSS Example</h1>
```
- **상속(Cascading)** : 상위 요소에 지정된 스타일 속성이 하위 요소로 전달되는 것
```css
<div class="parent"> <p class="child">Hello, World!</p> </div>
```
- **스타일 속성** : CSS에서는 HTML 요소에 적용되는 스타일을 지정하기 위해 다양한 속성을 제공한다. 예를 들어, color, font-size, background-color 등이 스타일 속성이다.
- **박스 모델** : CSS에서는 HTML 요소를 박스 형태로 취급하며, 박스 모델은 요소의 내용(content), 안쪽 여백(padding), 테두리(border), 바깥쪽 여백(margin)으로 구성된 것을 의미한다. 이를 이용하여 HTML 요소의 크기와 여백을 제어할 수 있다.
- **미디어 쿼리** : CSS에서는 화면의 크기에 따라 다른 스타일을 적용할 수 있는 미디어 쿼리를 지원한다. 예를 들어, 모바일 환경에서는 텍스트 크기를 작게하거나, 데스크톱 환경에서는 크게하거나 할 수 있다.
- **반응형 웹 디자인, 적응형 웹 디자인** : 반응형 웹 디자인은 감지된 화면 크기에 따라 자동으로 페이지가 재배열되는 유동적인 접근 방식이다. 적응형 웹 디자인은 브라우저가 주어진 플랫폼에 맞춰 특별히 생성된 레이아웃을 불러오는 웹 디자인 유형이다.



# flex
CSS의 레이아웃 모듈 중 하나, 요소들을 수평이나 수직 방향으로 쉽게 배치하고 정렬할 수 있도록 도와주는 기술이다. Flexbox를 사용하면 요소들을 빠르고 쉽게 배치할 수 있으며, 유연한 레이아웃을 만들 수 있다.
https://studiomeal.com/archives/197


# grid
flex와 마찬가지로 CSS 레이아웃 모듈 중 하나, 요소들을 행(row)와 열(column)로 배치하고 정렬할 수 있도록 도와주는 기술이다.
https://studiomeal.com/archives/533


# font-size
글자 크기로, \<font\> 태그의 size 속성과 효과가 같다.
(HTML5 부터 \<font\> 태그 사용은 권장되지 않으며, CSS를 사용해야 한다)
px, px, em, 등의 단위와 small, big 등의 상수 크기를 사용할 수 있다.
(일반 웹 페이지에서는 px 사용)
```html
<html>
<head>
	<style>
		#text1 { font-size: 37px }
		#text2 { font-size: 28px }
		#text3 { font-size: 19px }

		.bold { font-weight: bold }
		.italic{ font-style: italic }
		.jinji{ font-family: "궁서" }

		#text4{ font: italic bold 20px serif; }
   </style>
</head>
<body>
	<div id="text1">37px</div>
	<div id="text2">28px</div>
	<div id="text3">19px</div>
	<br>
	<div class="bold">굵은 글씨</div>
	<div class="italic">기울인 글</div>
	<div class="jinji">진지한 글꼴</div>
	<br>
	<div id="text4">There's no books on my backpack</div>
</body>
</html>
```


# color
글자의 색상을 변경한다.
- red, blue 등 이미 정의된 색
- #000, \#FFFFFF 등의 16진수 색상 코드
- rgb(255, 255, 255) 등의 rgb 색상
- rgba(200, 100, 150, 0.5) 등의 알파(투명도)가 적용된 rgba 색상
color 속성은 위 목록등의 값을 사용할 수 있으며, 기본값은 inherit 으로 부모의 색상을 가져온다.
```html
<html>
<body>
	<div style="color: red">text1</div>
	<div style="color: #0A0">text2</div>
	<div style="color: rgb(0, 0, 150)">text3</div>
	<div style="color: rgba(0, 140, 170, 0.5)">text4</div>
</body>
</html>
```


# margin, padding
margin 과 padding 속성은 각각 바깥쪽 여백, 안쪽 여백을 의미한다.
width, height 속성과 마찬가지로 숫자 뒤에 단위를 표시하여 적는다.

margin 과 padding 은 border 을 경계로 나뉜다.
<img src="https://ofcourse.kr/images/attach/margin_padding.png">
```html
<html>
<head>
<style>
	.box-container{
		display: inline-block;
		background-color: #d2f4ff;
		border: 2px solid #09c;
		margin: 5px 15px;
	}
	.box-container div{
		width: 120px;
		height: 80px;
		background-color: #fde6ff;
		border: 2px solid #90C;
		font-size: 15px;
	}
	#box1{ margin: 10px;  padding: 0; }
	#box2{ margin: 5px 25px; padding: 0; }
	#box3{ margin: 0;  padding: 10px 30px 5px; }
	#box4{ margin: 10px; padding: 10px 20px; }
	#box5{ margin: 10px 30px 0 50px; padding: 30px 0 }
</style>
</head>

<body>
	<div class="box-container">
		<div id="box1">m: 10<br>p: 0</div>
	</div>
	<div class="box-container">
		<div id="box2">m: 5 25<br>p: 0</div>
	</div>
	<div class="box-container">
		<div id="box3">m: 0<br>p: 10 30 5</div>
	</div>
	<div class="box-container">
		<div id="box4">m: 10<br>p: 10 20</div>
	</div>
	<div class="box-container">
		<div id="box5">m: 10 30 0 50<br>p: 30 0</div>
	</div>
</body>
</html>
```
https://ofcourse.kr/css-course/margin-padding-속성


# position
position 속성은 태그를 어떻게 위치시킬지를 정의하며, 아래의 5가지 값을 갖는다.
- **static** : 기본값, 다른 태그와의 관계에 의해 자동으로 배치되며 위치를 임의로 설정해 줄 수 없습니다.
- **absolute** : 절대 좌표와 함께 위치를 지정해 줄 수 있습니다.
- **relative** : 원래 있던 위치를 기준으로 좌표를 지정합니다.
- **fixed** : 스크롤과 상관없이 항상 문서 최 좌측상단을 기준으로 좌표를 고정합니다.
- **inherit** : 부모 태그의 속성값을 상속받습니다.
좌표를 지정 해주기 위해서는 left, right, top, bottom 속성과 함꼐 사용한다

position을 absolute 나 fixed 로 설정시 가로 크기가 100%가 되는 block 태그의 특징이 사라지게 된다.
```html
<html>
<head>
	<style>
		.box-container{
			width: 350px;
			border: 2px solid #e91bf5;
		}
		.box-container div{
			padding: 10px;
			border: 1px solid green;
			background-color: #e3ffe0;
		}
		#box1 { position: static; top: 20px; left: 30px; }
		#box2 { position: relative; top: 20px; left: 30px; }
		#box3 { position: absolute; top: 20px; right: 30px; }
		#box4 { position: fixed; top: 20px; right: 30px; }
	</style>
</head>
<body>
	<div class="box-container">
		<div id="box1">static 박스</div>
		<div id="box2">relative 박스</div>
		<div id="box3">absolute 박스</div>
		<div id="box4">fixed 박스</div> <!-- '출력 결과' 란이 아닌, 전체 페이지에서 고정되어 보여짐 -->
	</div>
</body>
</html>
```
