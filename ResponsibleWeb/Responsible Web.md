# 반응형 웹(Responsible Web)
반응형 웹은 하나의 웹 사이트에서 PC, 태블릿PC, 스마트폰 등 접속하는 디스플레이의 종류에 따라 화면의 크기가 자동으로 변하도록 만든 웹페이지 접근 기법을 말한다.
- 웹 사이트를 PC용과 태블릿PC, 모바일용으로 각각 제작하지 않고, 하나의 공용 웹 사이트를 만들어 다양한 디바이스에 대응할 수 있다는 장점이 있다.
- 웹 페이지의 내용을 수정할 경우, 하나의 웹 페이지만 수정하면 PC와 태블릿PC, 모바일 등 다양한 디바이스에서 동일하게 반영되는 장점이 있다.
- 반응형 웹의 핵심 기술은 가변 그리드, 유연한 이미지, 그리고 미디어 쿼리가 있다.
- 가장 많이 사용되고 있는 반응형 웹 제작 도구는 부트스트랩 프레임 워크가 있다.



## 1. 고정 그리드 레이아웃

<p align="center"><img src="../images/210429/16.gif"></p>

고정 그리드 레이아웃은 단위가 픽셀(px)이기 때문에 브라우저 크기가 확대/축소될 때 글자 및 웹 요소가 안 보이는 경우가 있다. 고정 그리드 레이아웃은 특정한 기기만 사용하고자 할 때 사용하면 유리하다. 레이아웃을 잡기가 상당히 수월하다.

```css
header {
	width: 960px;
	padding: 15px;
}
```



## 2. 가변 그리드 레이아웃

<p align="center"><img src="../images/210429/17.gif"></p>

```css
header {
	width: 100%;
	padding: 1.5625%;
}
```

### 2.1. 가변그리드 레이아웃 방식에서 각각의 요소의 너비를 구하는 공식(중요!) 
* (요소의 너비 / 컨텐츠 전체를 감싸는 요소의 너비) * 100 = (%)
요소를 백분율로 처리할 때 소수점 이하 값이 길게 나오는 경우에는 3-4자리정도로 끊어주는 것이 좋다.   


## 3. viewport 
viewport는 웹 페이지에서 사용자의 보이는 영역(visible area)이다.
사용자의 영역은 기기마다 달라진다.

```html
<meta name="viewport" content="width=device-width, initial-scale=1">
```

- width : viewport의 가로 크기.
- device-width : 기기의 스크린 너비에 맞추라는 의미.
- initial-scale : 웹 페이지에 접속했을 때 보여질 확대배율을 설정. 


## 4. rem

```css
.wrapper {
	width: 96%;
	margin: 0 auto;
	font-size: 12px;
}
	
.header_text {
	font-size: 2em;	
	/* 12px(부모 태그(.wrapper)의 폰트사이즈) * 2 = 24px */
}
	
.text {
	font-size: 1.5em;	/* 24px * 1.5 = 36px */
}
```

`.text`의 font-size는 36px이 나온다. 그 이유는 `em` 단위는 상위요소가 기준이 되어 사용이 되는데, 이 때 상위요소인 `header_text` 선택자 부분의 font-size가 24px이 되기 때문이다. 그로 인하여 복잡하게 프로그래밍을 하게 되면 글자 사이즈가 원하는 대로 출력이 어려워진다. 이것이 `em` 단위의 단점이다.  


그래서 이러한 단점을 대신하기 위해서 나온 단위가 `rem`이라는 단위이다.  


```css
body {
	font-size: 16px;	/* rem의 기준이 되는 기본 크기를 지정 */
}

.header_text {
	font-size: 2rem;	/* 16px * 2 = 32px */
}
	
.text {
	font-size: 1.5rem;	/* 16px * 1.5 = 24px */
}
```

`rem` 단위는 root 즉, `<body>` 태그를 처음부터 기본 크기로 지정하기 때문에 `em` 단위처럼 기본이 되는 크기가 중간에 변경되지 않는다.  
처음부터 끝까지 하나의 기본 사이즈를 기준으로 삼기 때문에 `em` 단위보다 간결하다.  



## 5. max-width
`width` 속성은 웹 문서에 삽입할 이미지의 너비 값을 표현하는 것이다.  
`max-width` 속성은 가변 이미지에서 최대한 표시할 수 있는 이미지의 너비값을 말한다. 브라우저 창의 너비를 줄이면 이미지도 같이 줄어든다.

```css
.content img {
	 max-width: 100%;
	 height: auto;
}
```


<p align="center"><img src="../images/210430/00.gif"></p>



비디오 파일에도 동일하게 적용 가능하다.

```css
video {
	max-width: 100%;
}
```


<p align="center"><img src="../images/210430/02.gif"></p>



## 6. srcset
* 형식) `srcset="파일 위치 [픽셀밀도][너비값]"`
	- `srcset` : 픽셀의 밀도와 너비값을 줄 수 있는 속성.
	- 픽셀밀도 : 픽셀이 얼마나 빽빽하게 차 있는지를 의미.


```html
<picture>
<!-- 1024px 이상은 large, 768~1024px은 medium, 320~768px은 small 이미지 표출  -->
	<source srcset="images/shop-large.jpg" media="(min-width:1024px)">
	<source srcset="images/shop-medium.jpg" media="(min-width:768px)">	
	<source srcset="images/shop-small.jpg" media="(min-width:320px)">
			
	<img src="images/shop.jpg" style="width: 100%">	
</picture>
```

캡쳐를 위해 해상도를 50%로 잡아 px은 작성코드와 다를 수 있다.  
<p align="center"><img src="../images/210430/01.gif"></p>



## 7. Media Query 미디어 쿼리
미디어 쿼리는 접속하는 장치(미디어)에 따라서 특정한 CSS 스타일을 사용하도록 하는 것을 말한다.

* `@media screen` : 미디어가 스크린일 때 CSS .
* `and (max-width: Npx)` : 최대 너비가 Npx 일 때 CSS 스타일. 여러 개 작성 시 내림차순으로 작성해야 한다.
* `and (min-width: Npx)` : 최소 너비가 Npx 일 때 CSS 스타일. 여러 개 작성 시 오름차순으로 작성해야 한다.


```css
/* 최대 너비 > 1024px 일 때는 bg0.jpg 파일을 body 태그의 배경 이미지로 설정 */
body {
	background: url("images/bg0.jpg") no-repeat fixed;
	background-size: cover;	/* 창크기에 딱 맞게 이미지 크기 설정 */
}

/* 768 < 최대 너비 <= 1024px 일 때는 bg1 이미지 깔기 */
@media screen and (max-width: 1024px) {
	body {
		background: url("images/bg1.jpg") no-repeat fixed;
		background-size: cover;
	}
}
	
/* 320px < 최대 너비 <= 768px 일 때는 bg2 이미지 깔기 */
media screen and (max-width: 768px) {
	body {
		background: url("images/bg2.jpg") no-repeat fixed;
		background-size: cover;
	}
}
	
/* 최대 너비 <= 320px 일 때는 bg3 이미지 깔기 */
@media screen and (max-width: 320px) {
	body {
		background: url("images/bg3.jpg") no-repeat fixed;
		background-size: cover;
	}
}
```


캡쳐를 위해 해상도를 50%로 잡아 px은 작성코드와 다를 수 있다.  
<p align="center"><img src="../images/210430/03.gif"></p>



```css
#wrap {
	height: 500px;
	margin: 0 auto;
	border: 3px solid #000;
}

@media screen and (min-width: 320px) {
	#wrap {
		width: 30%;
		background-color: green;
	}
} 

@media screen and (min-width: 768px) {
	#wrap {
		width: 60%;
		background-color: blue;
	}
}

@media screen and (min-width: 1024px) {
	#wrap {
		width: 90%;
		background-color: red;
	}
}
```


캡쳐를 위해 해상도를 50%로 잡아 px은 작성코드와 다를 수 있다.  
<p align="center"><img src="../images/210430/04.gif"></p>




