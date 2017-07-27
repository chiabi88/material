# Drawers

MDC Drawer 컴포넌트는 [Material Design navigation drawer pattern](https://material.io/guidelines/patterns/navigation-drawer.html)을 준수하는 정렬 된 드로어 컴포넌트이다.  
permanent(영구적인), persistent(지속적인), temporary(임시적인) 드로어를 구현한다.  
Permanent 드로어는 자바스크립트 필요없이 CSS만으로 구현하는 반면에 Persistent와 Temporary 드로어는 사용자 인터렉션에 반응하기 위해 자바스크립트가 작동해야한다.

> [원문](https://material.io/components/web/catalog/drawers/)  
> [데모 : Persistent Drawer](https://material-components-web.appspot.com/drawer/persistent-drawer.html)
> [데모 : Permanent Drawer Above Toolbar](https://material-components-web.appspot.com/drawer/permanent-drawer-above-toolbar.html)  
> [데모 : Permanent Drawer Below Toolbar](https://material-components-web.appspot.com/drawer/permanent-drawer-below-toolbar.html)  
> 

## 사용

### Permanent Drawer(영구적인 드로어)

영구적인 드로어는 항상 열려있고, 콘텐츠 측면에 있다.  
모바일보다 큰 크기의 디스플레이에 적합하다.

#### CSS classes:

| class | 설명 |
| ------ | ------ |
| mdc-premanent-drawer | _필수_. 컴포넌트의 루트 요소에 설정해야함 |
| mdc-premanent-drawer__content | _필수_. 드로어 콘텐츠의 컨테이너 노드에 설정해야함 |
| mdc-premanent-drawer__toolbar-spacer | _선택_. 노드에 추가해 툴바에 맞는 공간을 제공함 |

#### 영구적인 서랍을 툴바 위에 설정하는(Permanent Drawer Above Toolbar) 예 : 

toolbar spacer를 사용하여 툴바 높이와 정확히 일치하는 크기의 공백이 표시되도록 함  
toolbar spacer 안에 내용을 배치할 수 있다.

```html
<nav class="mdc-permanent-drawer mdc-typography">
  <div class="mdc-permanent-drawer__toolbar-spacer"></div>
  <div class="mdc-permanent-drawer__content">
    <nav id="icon-with-text-demo" class="mdc-list">
      <a class="mdc-list-item mdc-permanent-drawer--selected" href="#">
        <i class="material-icons mdc-list-item__start-detail" aria-hidden="true">inbox</i>Inbox
      </a>
      <a class="mdc-list-item" href="#">
        <i class="material-icons mdc-list-item__start-detail" aria-hidden="true">star</i>Star
      </a>
    </nav>
  </div>
</nav>
<div>
  Toolbar and page content go inside here.
</div>
```

#### 영구적인 서랍을 툴바 아래에 설정하는(Permanent Drawer Above Toolbar) 예 :

```html
<div>Toolbar goes here</div>

<div class="content">
  <nav class="mdc-permanent-drawer mdc-typography">
    <nav id="icon-with-text-demo" class="mdc-list">
      <a class="mdc-list-item mdc-permanent-drawer--selected" href="#">
        <i class="material-icons mdc-list-item__start-detail" aria-hidden="true">inbox</i>Inbox
      </a>
      <a class="mdc-list-item" href="#">
        <i class="material-icons mdc-list-item__start-detail" aria-hidden="true">star</i>Star
      </a>
    </nav>
  </nav>
  <main>
    Page content goes here.
  </main>
</div>
```

### Persistent Drawer(지속적인 드로어)

지속적인 드로어는 열거나 닫을 수 있다. 드로어는 컨텐츠와 동일한 엘리베이션 표면에 있다. 기본적으로 닫혀있다.  
드로어가 페이지 그리드 외부에 있고 열릴 때, 드로어는 더 작아진 뷰포트에 맞춰서 다른 컨텐츠 사이즈를 변경시킨다.  
지속적인 드로어는 사용자가 닫을때까지 열려있다.

모바일보다 큰 크기의 모든것에 적합하다.

#### CSS classes:

| class | 설명 |
| ------ | ------ |
| mdc-persistent-drawer | _필수_. 컴포넌트의 루트 요소에 설정해야함 |
| mdc-persistent-drawer__drawer | _필수_. 드로어 콘텐츠의 컨테이너 노드에 설정해야함 |

```html
<aside class="mdc-persistent-drawer mdc-typography">
  <nav class="mdc-persistent-drawer__drawer">
    <header class="mdc-persistent-drawer__header">
      <div class="mdc-persistent-drawer__header-content">
        Header here
      </div>
    </header>
    <nav id="icon-with-text-demo" class="mdc-persistent-drawer__content mdc-list">
      <a class="mdc-list-item mdc-persistent-drawer--selected" href="#">
        <i class="material-icons mdc-list-item__start-detail" aria-hidden="true">inbox</i>Inbox
      </a>
      <a class="mdc-list-item" href="#">
        <i class="material-icons mdc-list-item__start-detail" aria-hidden="true">star</i>Star
      </a>
    </nav>
  </nav>
</aside>
```

### Temporary drawer usage

임시적인 드로어는 일반적으로 닫혀있고, 열릴 때 컨텐츠 보다 높은 엘리베이션에 슬라이딩하여 나타난다.  
모든 사이즈의 디바이스에 적합하다.

```html
<aside class="mdc-temporary-drawer mdc-typography">
  <nav class="mdc-temporary-drawer__drawer">
    <header class="mdc-temporary-drawer__header">
      <div class="mdc-temporary-drawer__header-content">
        Header here
      </div>
    </header>
    <nav id="icon-with-text-demo" class="mdc-temporary-drawer__content mdc-list">
      <a class="mdc-list-item mdc-temporary-drawer--selected" href="#">
        <i class="material-icons mdc-list-item__start-detail" aria-hidden="true">inbox</i>Inbox
      </a>
      <a class="mdc-list-item" href="#">
        <i class="material-icons mdc-list-item__start-detail" aria-hidden="true">star</i>Star
      </a>
    </nav>
  </nav>
</aside>
```

#### Headers and toolbar spacers

임시적인 드로어는 툴바 스페이서, 헤더 또는 둘다 사용할 수 있다.

## slidable

MDC Slideable Drawer는 슬라이드 인 서랍의 하위 클래스로, 일명 '영구 및 임시 서랍'이다.  
터치 및 전환 이벤트를 처리하는 JavaScript 로직을 유지 관리한다.  
이것은 공개 API가 아니다. 영구 서랍과 임시 서랍의 논리를 동기화하는 것을 의미한다.

### Variables 

transition 시간 관련 변수
```scss
$mdc-slidable-drawer-transition-time: .13s;
$mdc-slidable-drawer-transition-open-time: .33s;
```

**mdc-animation** 의 함수에 transform 속성과, slidable 변수의 시간을 인수로 넣어 트랜지션 속성 정의  
```scss

$mdc-slidable-drawer-transition: mdc-animation-enter(transform, $mdc-slidable-drawer-transition-time);
$mdc-slidable-drawer-transition-open: mdc-animation-enter(transform, $mdc-slidable-drawer-transition-open-time);
```

```scss
// "@material/animation/functions";

@function mdc-animation-enter($name, $duration, $delay: 0ms) {
  @return $name $duration $delay $mdc-animation-linear-out-slow-in-timing-function;
}
```

### [mixin] mdc-slidable-drawer

```scss
@mixin mdc-slideable-drawer {
  height: 100%;
  transform: translateX(-107%);
  transform: translateX(calc(-100% - 20px));
  will-change: transform;
}
```

### [mixin] mdc-slideable-drawer-rtl
```scss
@mixin mdc-slideable-drawer-rtl {
  transform: translateX(107%);
  transform: translateX(calc(100% + 20px));
}
```

### [mixin] mdc-slideable-drawer-open
```scss
@mixin mdc-slideable-drawer-open {
  transform: none;
}
```
***

+ [머티리얼 디자인 : 네비게이션 드로어](http://davidlab.net/google-design-ko/patterns/navigation-drawer.html)
+ [머티리얼 디자인 : 엘리베이션과 그림자](http://davidlab.net/google-design-ko/what-is-material/elevation-shadows.html)