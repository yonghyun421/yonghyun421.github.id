---
date: '2021-11-13'
title: 'useMediaQuery'
categories: ['React', 'TIL', 'useMediaQuery', '반응형']
summary: '반응형 아직도 안써?'
thumbnail: './images/usemediaquery.jpeg'
---

# 반응형 웹(responsive Web)이란?

반응형 웹은 모바일,태블릿,pc 등 다양한 종류의 디바이스에 따라 웹페이지의 크기가 자동적으로 재조정 되는 것을 말한다. 즉 어떠한 환경에서도 그에 맞게 사이즈가 변화되어 사용자가 보기 편리하게 만드는 웹이다.

## 미디어 쿼리(Media Query)

CSS2.1부터 미디어 타입으로 단말기 종류에 따라 각각 다른 스타일을 적용 시키는게 가능했다. 하지만 미디어 타입만으로는 해당 기기의 특성을 정확히 판단하기가 어려워 많이 사용되지는 않았다. CSS3은 위의 미디어 타입을 개선하여, 좀 더 구체적인 조건으로 필요한 스타일을 적용할 수 있도록 확장하였는데 이를 `미디어 쿼리`라고 한다.

### react-responsive

- useMediaQuery를 사용하기 위해선 react-responsive를 설치해야 함
- `npm i react-responsive`

### 미디어 쿼리 적용시키기

#### 1. `<link>`

`<link>` 태그는 `<head>` 태그 안에 위치하여 media 속성 안 조건에 만족할 때 해당 CSS 파일을 불러온다.

```html
<link href="style.css" media="screen and (min-width: 512px) rel="stylesheet"/>
```

#### 2. `<style>`

`<style>` 태그는 `<head>` 태그 안에 위치하여 media 속성 안 조건에 만족 할 때 스타일을 적용 시킨다.

```html
<style href="style.css" media="screen and (min-width: 512px) rel="stylesheet">
/*style*/
    p{
    	width: 300px;
        height: 100px;
    }
</style>

```

#### 3. `<style> - @import`

`<style>` 태그 안에서 @import를 사용하여 뒷 부분의 미디어 쿼리를 만족 할 때 해당 CSS 파일을 불러온다.

```html
<style>
  @import url(style.css) screen and (min-width: 512px);
</style>
```

#### 4. CSS 파일

```css
@media screen and (min-width: 512px) and (max-width: 1024px) {
  p {
    width: 200px;
    backgroud: #ffffff;
  }
}
```

### 미디어 쿼리 문법

![](https://images.velog.io/images/4_21ee/post/4916cd87-4581-47bd-bf0b-2d1fabd88f2a/image.png)
only|not의 위치에는 말 그대로 only 키워드 또는 not 키워드가 들어가게 되는데 only 키워드는 뒤의 조건만, not 키워드는 뒤의 조건을 제외한 조건을 뜻한다. 미디어 쿼리를 지원하지 않는 브라우저의 경우 only 키워드가 쿼리 안의 내용이 무시되어 실행 되지 않는다.
only 키워드는 큰 의미는 없지만 미디어 쿼리를 지원하는 브라우저를 대상으로 할 경우 적어주는 것이 좋다.

### 미디어 타입의 종류

- **`all`** : 모든 미디어 타입
- `aural` : 음성 합성장치
- `braille` : 점자 표시 장치
- `handheld` : 손으로 들고 다니면서 볼 수 있는 작은 스크린에 대응하는 용도
- **`print`** : 인쇄 용도
- `projection` : 프로젝터
- **`screen`** : 컴퓨터 스크린
- `tty` : 디스플레이 능력이 한정된 텔렉스, 터미널, 또는 수동 이동 장치등 고정 된 글자를 사용하는 미디어
- `tv` : 음성과 영상이 동시 출력 되는 장치
- `embrossed` : 페이지에 인쇄된 점자 표지 장치
  _**\*모바일 기기는 handheld가 아닌 screen이다!!**_

### 미디어 쿼리문의 속성

- `width` : 웹페이지의 가로 길이를 판단
- `height` : 웹페이지의 세로 길이를 판단
- `device-width` : 단말기의 물리적인 가로길이를 판단
- `device-height` : 단말기의 물리적인 세로길이를 판단
- `orientation` : width와 height을 구하여 width 값이 길면 landscape로 height 값이 길면 portrait로 판단
- `aspect-ratio` : width/height 비율을 판단
- `device-aspect-ratio` : 단말기의 물리적인 화면 비율을 판단
- `color-index` : 단말기에서 사용하는 최대 색상수를 판단
- `monochrom` : 흑백 컬러만을 사용하는 단말기에서 흰색과 검은색 사이의 단계를 판단
- `resolution` : 지원하는 해상도를 판단
- `color` : 단말기에서 사용하는 최대 색상 수의 비트 수를 판단

미디어 쿼리 속성은 프로그래밍 언어와 같이 =,>,< 등의 연산자를 사용하지 않으며 속성명 앞에 `min-` 또는 `max-` 를 붙여서 최소값, 최대값을 판단한다. 속성은 `and (속성:속성값) and (속성:속성값)` 으로 나열 할 수 있고 `min-`, `max-`를 이용할 경우 범위로도 설정 가능하다.

### 미디어쿼리 사용예제

![](https://images.velog.io/images/4_21ee/post/6549592f-bb68-474f-a07e-e24ea3783139/image.png)

```html
<html>
  <head>
    <style>
      div{
      	width: 100%;
      	height: 100%;
      }
      @media screen and (max-width : 100px){
      	div{background-color : blue;}
      @media screen and (min-width : 100px) and (max-width : 200px){
      	div{background-color : red;}
      @media screen and (min-width : 200px){
      	div{background-color : green;}
      }
    </style>
  </head>
  <body>
    <div></div>
  </body>
</html>
```
