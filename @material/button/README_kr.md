<!--docs:
title: "Buttons"
layout: detail
section: components
excerpt: "Material Design-styled buttons."
iconId: button
path: /catalog/buttons/
-->

# Buttons

<!--<div class="article__asset">
  <a class="article__asset-link"
     href="https://material-components-web.appspot.com/button.html">
    <img src="{{ site.rootpath }}/images/mdc_web_screenshots/buttons.png" width="363" alt="Buttons screenshot">
  </a>
</div>-->

The MDC Button 컴퍼넌트는 [Material Design button requirements](https://material.io/guidelines/components/buttons.html)를 준수하는 맞춤정렬 버튼 컴포넌트이다..
이 작업은 자바스크립트 없이 기본기능을 포함한다.
버튼에 대해 javascript object 를 시작할경우  향상된 ripple effects를 볼수있다.(아직 구현되지 않음)

## Design & API Documentation

<ul class="icon-list">
  <li class="icon-list-item icon-list-item--spec">
    <a href="https://material.io/guidelines/components/buttons.html">원문</a>
  </li>
  <li class="icon-list-item icon-list-item--link">
    <a href="https://material-components-web.appspot.com/button.html">데모 - Button</a>
  </li>
</ul>

## Installation

```
npm install --save @material/button
```

## Usage

### Flat

```html
<button class="mdc-button">
  Flat button
</button>
```

### Colored

```html
<button class="mdc-button mdc-button--accent">
  Colored button
</button>
```

### Raised

```html
<button class="mdc-button mdc-button--raised">
  Raised button
</button>
```

### Disabled

```html
<button class="mdc-button mdc-button--raised" disabled>
  Raised disabled button
</button>
```

###  버튼에 ripple effect 추가
버튼에 ripple effect 를 추가하려면 button elemnet 에 ripple 인스턴스를 붙인다.

```js
mdc.ripple.MDCRipple.attachTo(document.querySelector('.mdc-button'));
```
 [material-components-web](../material-components-web) package를 사용할때 이것을 선언적으로 수행할수 있다.


```html
<button class="mdc-button" data-mdc-auto-init="MDCRipple">
  Flat button
</button>
```
buttons 는 ripple style을 완벽하게 지원함으로 dom 이나 css 를 변경하지 않아도 됨.

## Classes

### Block
블럭 class 는 'mdc-button' 이다. 이는 최상위 버튼요소를 정의한다.


### Element
button component 에는 inner elemnet 가 없다.


### Modifier

The provided modifiers are:

| Class                 | Description                                             |
| --------------------- | ------------------------------------------------------- |
| `mdc-button--dense`   | 버튼 텍스트를 약간 작게 압축한다.                               |
| `mdc-button--raised`  | 버튼을 올리고, 배경색을 만든다.                                |
| `mdc-button--compact` | 버튼 가로패팅양을 줄임                                        |
| `mdc-button--primary` | primary color 컬러 지정                                    |
| `mdc-button--accent`  | accent color 컬러 지정                                     |
