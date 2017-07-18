<!--docs:
title: "Animation"
layout: detail
section: components
excerpt: "Animation timing curves and utilities for smooth and consistent motion."
iconId: animation
path: /catalog/animation/
-->

# Animation

MDC Animation은 Sass / CSS / JavaScript 라이브러리로 Material Design 애니메이션을위한 툴 벨트<sup>toolbelt</sup>를 제공한다. [motion guidelines](https://material.io/guidelines/motion/duration-easing.html#duration-easing-common-durations). 현재는 easing curves만 커버한다.

## Design & API Documentation

+ [Material Design guidelines: Duration & easing](https://material.io/guidelines/motion/duration-easing.html)

## Installation

```
npm install --save @material/animation
```

## Usage

### Variables

현재 다음 3 가지 애니메이션 커브에 대한 변수가 있다.

| Variable name | timing function | use case |
| --- | --- | --- |
| `$mdc-animation-fast-out-slow-in-timing-function` | `cubic-bezier(.4, 0, .2, 1)` | 표준 곡선; 처음부터 끝까지 볼 수있는 모든 애니메이션 (e.g. FAB에서 툴바로 변환) |
| `$mdc-animation-linear-out-slow-in-timing-function` | `cubic-bezier(0, 0, .2, 1)` | 객체가 화면에 들어가게하는 애니메이션 (e.g. 페이드 인) |
| `$mdc-animation-fast-out-linear-in-timing-function` | `cubic-bezier(.4, 0, ``, 1)` | 객체가 화면을 떠나는 애니메이션 (e.g. 페이드 아웃) |

> FAB : [Floating Action Button](https://material.io/guidelines/components/buttons-floating-action-button.html)

mdc-animation을 빌드에 넣기 만하면된다.

```scss
.mdc-thing--animating {
  animation: foo 175ms $mdc-animation-fast-out-slow-in-timing-function;
}
```

또는 해당 변수를 단순히 animation-timing-function 속성에 할당하는 믹스인을 사용한다. :

```scss
.mdc-thing--on-screen {
  @include mdc-animation-fast-out-linear-in;
}
```
### Mixin

모든 mixin은 `-timing-function` 접미사가 없이 해당 변수와 동일한 이름을 가진다.

```scss
@mixin mdc-animation-linear-out-slow-in {
  animation-timing-function: $mdc-animation-linear-out-slow-in-timing-function;
}

@mixin mdc-animation-fast-out-slow-in {
  animation-timing-function: $mdc-animation-fast-out-slow-in-timing-function;
}

@mixin mdc-animation-fast-out-linear-in {
  animation-timing-function: $mdc-animation-fast-out-linear-in-timing-function;
}
```

### Functions

MDC Animation은 무언가가 프레임에 들어가고 빠져 나올 때를 위한 트랜지션을 정의하는 도우미 함수를 제공한다.  

```scss
@function mdc-animation-enter($name, $duration, $delay: 0ms) {
  @return $name $duration $delay $mdc-animation-linear-out-slow-in-timing-function;
}

@function mdc-animation-exit($name, $duration, $delay: 0ms) {
  @return $name $duration $delay $mdc-animation-fast-out-linear-in-timing-function;
}
```

매우 일반적인 예는 불투명도를 사용하여 페이드 인 한 다음 페이드 아웃하는 것이다.

```scss
@import "@material/animation/functions";

.mdc-thing {
  transition: mdc-animation-exit(/* $name: */ opacity, /* $duration: */ 175ms, /* $delay: */ 150ms);
  opacity: 0;
  will-change: opacity;

  &:active {
    transition: mdc-animation-enter(opacity, 175ms /*, $delay: 0ms by default */);
    opacity: 1;
  }
}
```
```css
/* css 컴파일 */
.mdc-thing {
  transition: opacity 175ms 150ms cubic-bezier(0.4, 0, 1, 1);
  opacity: 0;
  will-change: opacity;
}

.mdc-thing:active {
  transition: opacity 175ms 0ms cubic-bezier(0, 0, 0.2, 1);
  opacity: 1;
}
```

이 함수는 `animation` 속성에서도 작동한다.

```scss
@import "@material/animation/functions";

@keyframes fade-in {
  from {
    transform: translateY(-80px);
    opacity: 0;
  }

  to {
    transform: translateY(0);
    opacity: 1;
  }
}

.mdc-thing {
  animation: mdc-animation-enter(fade-in, 350ms);
}
```
```css
/* css 컴파일 */
@keyframes fade-in {
  from {
    transform: translateY(-80px);
    opacity: 0;
  }
  to {
    transform: translateY(0);
    opacity: 1;
  }
}

.mdc-thing {
  animation: fade-in 350ms 0ms cubic-bezier(0, 0, 0.2, 1);
}
```

### CSS Classes

> NOTE: dist/ 는 NPM을 통해 설치할 때 사용할 수 있다.

빌드 된 스타일 시트를 인클루드하고 HTML에서 클래스를 사용할 수 있다.

```html
<link href="path/to/mdc-animation/dist/mdc-animation.css" rel="stylesheet">
<!-- ... -->
<div id="my-animating-div" class="mdc-animation-fast-out-slow-in">hi</div>
```

CSS 클래스는 믹스 인 클래스와 정확히 같은 이름을 가지고 있다.

### 기본 curves를 재정의한다.(Overriding the default curves).

모든 애니메이션 변수는! default로 표시되므로 필요한 경우 재정의 할 수 있다.

### JavaScript

MDC 웹에는 애니메이션을보다 쉽게 ​​구현할 수 있도록 설계된 유틸리티 함수 세트가 함께 제공된다.

### Using Utility Functions

To use:
```js
import {getCorrectEventName} from '@material/animation';

const eventToListenFor = getCorrectEventName(window, 'animationstart');
```

| Method Signature | Description |
| --- | --- |
| `getCorrectEventName(windowObj: Object, eventType: string)` | JavaScript 이벤트 이름을 반환한다. 필요한 경우 접두사. |
| `getCorrectPropertyName(windowObj: Object, eventType: string)` | CSS 프로퍼티 명을 반환한다. 필요한 경우 접두사. |