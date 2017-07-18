<!--docs:
title: "RTL"
layout: detail
section: components
excerpt: "Right-to-left and bi-directional text layout via SCSS helpers."
path: /catalog/rtl/
-->

# RTL

MDC RTL은 MDC-Web components의 RTL / 양방향 레이아웃을 지원하기 위해 믹스인을 제공한다. 
MDC-Web 전반에 걸쳐 RTL에 대한 표준 접근법을 구현하고자하므로 RTL 지원이 필요한 모든 MMDC-Web component가 이 패키지를 활용할 것을 적극 권장한다.

## Design & API Documentation

+ [Material Design guidelines: Bidirectionality](https://material.io/guidelines/usability/bidirectionality.html)</a>

## Installation

```
npm install --save @material/rtl
```

## Usage

간단히 `@import "@material/rtl/mixins";` 하고 믹스인을 사용하라, 각 믹스인 설명은 아래에 있다.

### mdc-rtl

```scss
@mixin mdc-rtl($root-selector: null)
```

MDC-Web component가 RTL 레이아웃의 컨텍스트 내에 있을 때 적용될 규칙을 만든다.

```scss
@mixin mdc-rtl($root-selector: null) {
  // 지정된 루트 셀렉터가 있으면
  @if ($root-selector) {
    // 최상위 루트에 블록 안 구문을 내보낸다.
    // '[dir="rtl"] 지정루트셀렉터 부모요소참조, 지정루트셀렉터[dir="trl"] 부모요소참조'
    @at-root {
      [dir="rtl"] #{$root-selector} &,
      #{$root-selector}[dir="rtl"] & {
        @content;
      }
    }
  }
  // 지정된 루트 셀렉터가 없으면 '[dir="rtl"] 부모요소참조, 부모요소참조[dir="trl"]' 에 스타일을 지정한다.
  @else {
    [dir="rtl"] &,
    &[dir="rtl"] {
      @content;
    }
  }
}
```
Usage Example:

```scss
.mdc-foo {
  position: absolute;
  left: 0;

  @include mdc-rtl {
    left: auto;
    right: 0; // right 기준으로
  }

  &__bar {
    margin-left: 4px;
    @include mdc-rtl(".mdc-foo") {
      margin-left: auto;
      margin-right: 4px;
    }
  }
}

.mdc-foo--mod {
  padding-left: 4px;

  @include mdc-rtl {
    padding-left: auto;
    padding-right: 4px;
  }
}
```

css 컴파일:

```css
.mdc-foo {
  position: absolute;
  left: 0;
}
[dir="rtl"] .mdc-foo, .mdc-foo[dir="rtl"] {
  left: auto;
  right: 0;
}
.mdc-foo__bar {
  margin-left: 4px;
}
[dir="rtl"] .mdc-foo .mdc-foo__bar, .mdc-foo[dir="rtl"] .mdc-foo__bar {
  margin-left: auto;
  margin-right: 4px;
}

.mdc-foo--mod {
  padding-left: 4px;
}
[dir="rtl"] .mdc-foo--mod, .mdc-foo--mod[dir="rtl"] {
  padding-left: auto;
  padding-right: 4px;
}
```
**N.B.**:  조상 엘리먼트의 [dir="rtl"] 확인은 대부분의 경우 동작하지만, 복잡한 레이아웃의 경우 부정적인 결과를 초래할 수 있다., e.g.

```html
<html dir="rtl">
  <!-- ... -->
  <div dir="ltr">
    <div class="mdc-foo">Styled incorrectly as RTL!</div>
  </div>
</html>
```

불행히도, 우리는 이것이 지금 우리가 할 수있는 최선이라는 것을 발견했다. 앞으로는 : [:dir](http://mdn.io/:dir) 같은 선택자가 이 문제를 완화하는 데 도움이 될 것이다.

### mdc-rtl-reflexive-box

```scss
@mixin mdc-rtl-reflexive-box($base-property, $default-direction, $value, $root-selector: null)
```

기본 box-model 속성 (e.g. margin / border / padding) 에 기본 방향, 값을 지정하고 default로  `# $ base-property}-#{$ default-direction}` 속성에 값을 적용하는 규칙을 내보내지만, RTL context 내에서는 방향을 반전한다.

```scss
// $base-property : 박스모델 속성(margin / border/ padding)
// $default-direction : 기본 방향 값 (left / right)
// $value : 박스모델 속성 방향 속성에 넣을 값
@mixin mdc-rtl-reflexive-box($base-property, $default-direction, $value, $root-selector: null) {
  // $default-direction값이 right, left 중에 없으면 에러를 출력
  @if (index((right, left), $default-direction) == null) {
    @error "Invalid default direction #{default-direction}. Please specifiy either right or left";
  }
  // $left-vaule 에 값을 저장하는데
  $left-value: $value;
  $right-value: 0;

  // 만약 $default-direction 값이 right면 $right-value에 $value 값을 저장 
  @if ($default-direction == right) {
    $left-value: 0;
    $right-value: $value;
  }
  // mdc-rtl-reflexive-property 믹스인 사용
  @include mdc-rtl-reflexive-property($base-property, $left-value, $right-value, $root-selector);
}
```

For example:

```scss
.mdc-foo {
  @include mdc-rtl-reflexive-box(margin, left, 8px);
}
```
다음과 같다. :

```scss
.mdc-foo {
  margin-left: 8px;

  @include mdc-rtl {
    margin-right: 8px;
    margin-left: 0;
  }
}
```

반대로하면 :

```scss
.mdc-foo {
  @include mdc-rtl-reflexive-box(margin, right, 8px);
}
```
다음과 같다. :

```scss
.mdc-foo {
  margin-right: 8px;

  @include mdc-rtl {
    margin-right: 0;
    margin-left: 8px;
  }
}
```

`mdc-rtl`에 전달 될 4번째 선택적인 인자(`$root-selector`)를 전달할 수도 있다.

e.g. `@include mdc-rtl-reflexive-box-property(margin, left, 8px, ".mdc-component")`.

이 함수는 항상 RTL context의 원래 값을 0으로 만든다.  
값을 뒤집으려면 `mdc-rtl-reflexive-property`를 사용하라.

### mdc-rtl-reflexive-property

```scss
@mixin mdc-rtl-reflexive-property($base-property, $left-value, $right-value, $root-selector: null)
```
기본 속성을 취하고 LTR context 에서 `#{$ base-property}`-left를 `#{left-value}`로, 
`#{base-property}`-right를 `#{right-value}`로 할당하는 규칙을 내보내며 LTR context에서 그 반대의 경우도 마찬가지이다.

```scss
@mixin mdc-rtl-reflexive-property($base-property, $left-value, $right-value, $root-selector: null) {
  $prop-left: #{$base-property}-left;
  $prop-right: #{$base-property}-right;

  @include mdc-rtl-reflexive_($prop-left, $left-value, $prop-right, $right-value, $root-selector);
}
```

For example:

```scss
.mdc-foo {
  @include mdc-rtl-reflexive-property(margin, auto, 12px);
}
```
다음과 같다:

```scss
.mdc-foo {
  margin-left: auto;
  margin-right: 12px;

  @include mdc-rtl {
    margin-left: 12px;
    margin-right: auto;
  }
}
```

A 4th optional $root-selector argument can be given, which will be passed to `mdc-rtl`.

### mdc-rtl-reflexive-position

```scss
@mixin mdc-rtl-reflexive-position($pos, $value, $root-selector: null)
```

Takes an argument specifying a horizontal position property (either "left" or "right") as well
as a value, and applies that value to the specified position in a LTR context, and flips it in a
RTL context.

For example:

```scss
.mdc-foo {
  @include mdc-rtl-reflexive-position(left, 0);
  position: absolute;
}
```
is equivalent to:

```scss
 .mdc-foo {
   position: absolute;
   left: 0;
   right: initial;

   @include mdc-rtl {
     right: 0;
     left: initial;
   }
 }
```

An optional third `$root-selector` argument may also be given, which is passed to `mdc-rtl`.
