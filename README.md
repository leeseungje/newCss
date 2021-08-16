# 최신 CSS 기능 5가지

## @supports
- 브라우저가 해당 css를 지원하는지 여부를 확인 해 주는 기능.
```CSS
 @supports(property-name: property-value) { /* property-name을 지원하는 css 경우 */
    .box {
        property-name: property-value
    }
}
@supports not(property-name: property-value) { /* property-name을 브라우저에서 지원하지 않는 css 경우 */
    .box {
        property-name: property-value
    }
}
@supports( property-name: property-value ) and ( property-name: property-value ) {  /* property-name이 두개 이상의 표현식이 지원하는 css일 경우 */
    .box {
        property-name: property-value
    }
}
@supports( property-name: property-value ) or ( property-name: property-value ) { /* property-name이 한개 이상의 표현식의 결과가 맞을경우 */
    .box {
        property-name: property-value
    }
}
@supports selector(A > B) { /* 직계 자손 선택자 지원하는 브라우저 */
    .container > .box {
        property-name: property-value
    }
}
```
- [예제](https://jsfiddle.net/myubbak/cg0r6m45/3/)
- [지원 브라우저](https://caniuse.com/?search=%40supports)
- [테스트 코드](https://github.com/leeseungje/newCss/blob/main/support.html)


## css scroll snap
- js로 넣어야 했던 scroll page이동을 css로 구현이 가능한 기능.
- 사용자가 터치 및 휠 마우스를 조작하여 스크롤링하면 부모영역에서 scroll snap이 동작.
- 부모의 영역에 속성값 `scroll-snap-type`을 넣고 자식의 영역 속성에 `scroll-snap-align`을 넣으면 된다.
- 기타 속성에 `scroll-padding`, `scroll-margin` 기능이 있다.
### scroll-snap-type
```css
scroll-snap-type: x mandatory; /* 가로축 snap position */
scroll-snap-type: y proximity; /* 세로축 snap position */
scroll-snap-type: both mandatory; /* 두 축의 위치를 지정 */
```
- `mandatory`: 항상 snap
- `proximity`: snap position(scroll-snap-align)을 지정했다면 해당 설정에 맞춰 snap하지만, 미지정 상태면 유저 에이전트에 따름
### scroll-snap-align
```css
scroll-snap-align: start; /* snap position을 시작 부분에 정렬 */
scroll-snap-align: center; /* snap position을 가운에 정렬 */
scroll-snap-align: end; /* snap position을 끝 부분에 정렬 */
```
- snap 포지션이 area안에서 원하는 정렬로 설정이 가능함.
![scroll-snap-align 위치 - 출처: https://wit.nts-corp.com/2018/08/28/5317](https://github.com/leeseungje/newCss/blob/main/img/snap-position.gif "scroll-snap-align 위치 - 출처: https://wit.nts-corp.com/2018/08/28/5317")

### scroll-padding
```css
scroll-padding: npx;
```
- 부모 영역에 속성을 넣으며 해당 영역만큼(`npx`) 공간이 확보됨
- 안에 contents 내용과 padding 영향을 미치지 않음
### scroll-margin
```css
scroll-margin: npx;
```
- 자식 영역에 속성을 넣으며 scroll-padding속성과 비슷하지만 개별 section에 따로따로 속성을 부여할 수 있다.
- 안에 contents 내용과 padding 영향을 미치지 않음

- [예제](https://jsfiddle.net/myubbak/9vmokbta/2/)
- [지원 브라우저-scroll-snap-type](https://caniuse.com/?search=scroll-snap-type), [지원 브라우저-scroll-snap-type](https://caniuse.com/?search=scroll-snap-align)
- [테스트 코드](https://github.com/leeseungje/newCss/blob/main/scroll-snap.html)

## :is pseudo selector
```css
:is(header, main, footer) p:hover {
    property-name: property-value
}

/*  */
header p:hover,
main p:hover,
footer p:hover {
  color: red;
  cursor: pointer;
}
```
- 가상 클래스의 함수 다수 선택자
- is도 있지만 `where` 비슷한 기능이 있다.
- [css selectors level4](https://css4-selectors.com/selectors/)
### is(Matches-any pseudo-class) 모든 유사 클래스와 일치
- `:is`내부의 선택자는 전체 선택자의 특이성에 포함되어 다른 클래스 요소 선택자보다 더 높은 특이성을 가지고 있다.
### where(Matches-any pseudo-class) 특이성 조정 의사 클래스
- 반대로 `:where`는 내부의 선택자 특이성이 0이라 간단한 선택에 무시 된다.
```css
:is(header.is, main.is, footer.is) h1 {
    color: #fff;
}
:where(header.where, main.where, footer.where) h1 {
    color: blue;
}
footer h1 { /* is는 반영 되지 않고 where속성만 먹는다. */
    color: orange;
}
```
- [예제](https://jsfiddle.net/myubbak/k43tvnm7/4/)
- [지원 브라우저](https://caniuse.com/?search=%3Ais)
- [테스트 코드](https://github.com/leeseungje/newCss/blob/main/is.html)

## flex box gap
```css
.parent {
    display: flex;
    flex-wrap: wrap;
    gap: 10px 20px;
}
.children {
    width: 180px;
    height: 180px;
    background: orchid;
    display: inline-flex;
    align-items: center;
    justify-content: center;
    font-size: 20px;
    color: #fff;
}
```
- flex layout 간격을 margin이 아닌 gap 프로퍼티를 주는 기능
- margin은 존재 여부와 상관 없이 항상 스타일이 사용 된다면 gap은 인접한 요소가 없으면 불필요한 공간을 만들지 않는다.
- gap의 요소는 부모에 속성을 부여하며 상하, 좌우 까지 속성값을 입력 할 수 있다.

- [예제](https://jsfiddle.net/myubbak/2p3qnyhs/1/)
- [지원 브라우저](https://caniuse.com/?search=gap)
- [테스트 코드](https://github.com/leeseungje/newCss/blob/main/gap.html)

## aspect-ratio
```css
.element {
  aspect-ratio: 2 / 1; /* ↔️ is double the ↕️ */
}

.element {
  aspect-ratio: 1 / 1; /* ⏹ a perfect square */
}
```
- 반응형 사이트에서 영상 혹은 이미지를 보여줄때 정해진 비율을 유지하고 싶을때 쓰는 기능
- padding, calc로 속성을 넣을 수 있지만 수학적인 계산법 때문에 시간이 많이 요소가 됨
```css
.ratio {
    overflow: hidden;
    position: relative;
    height: 0;
}
.ratio.padding {
    padding-top: 56.25%; /* 16:9 */
}
.ratio.calc {
    padding-top:  calc(591.44  /  1127.34  *  100%); /* 16:9 */
}
.ratio.ratio {
    aspect-ratio: 16 / 9; /* 16:9 */
}
img {
    position: absolute; /* padding, calc 일때만 사용 */
    left: 0; /* padding, calc 일때만 사용 */
    top: 0; /* padding, calc 일때만 사용 */
    width: 100%;
    height: 100%;
}
```
- media query 로도 활용이 가능하다.
```css
/* Minimum aspect ratio */
@media (min-aspect-ratio: 8/5) {
  div {
    background: #9af; /* blue */
  }
}

/* Maximum aspect ratio */
@media (max-aspect-ratio: 3/2) {
  div {
    background: #9ff;  /* cyan */
  }
}

/* Exact aspect ratio, put it at the bottom to avoid override*/
@media (aspect-ratio: 1/1) {
  div {
    background: #f9a; /* red */
  }
}
```
- [예제](https://jsfiddle.net/myubbak/f1xutobL/7/)
- [지원 브라우저](https://caniuse.com/?search=aspect-ratio)
- [테스트 코드](https://github.com/leeseungje/newCss/blob/main/aspect-ratio.html)

## :sticky
```css
html, body {
    margin: 0;
    padding: 0;
    display: overlay;
}
.parent {
    width: 100%;
    height: 200vh;
    border: 10px solid saddlebrown;
    box-sizing: border-box;
    margin-bottom: 100px;
}
header {
    position: -webkit-sticky; /* 사파리 브라우저 지원 */
    position: sticky;
    left: 0;
    top: 0;
    height: 100px;
    background: royalblue;
    color: #fff;
}
header.second {
    background: orchid;
}
```
- 해당 엘레먼트를 사용하면 스크롤 위치가 임계점에 이르면 fixed와 같이 박스를 화면에 고정할 수 있는 속성
- fixed는 뷰포트에 고정이지만 sticky박스는 scroll박스에 고정.
- `top`,`left`,`bottom`,`right` 속성이 필수
- 현재 목표그룹 테이블에서 사용 중

- [예제](https://jsfiddle.net/myubbak/8bd1oeua/2/)
- [지원 브라우저](https://caniuse.com/?search=sticky)
- [테스트 코드](https://github.com/leeseungje/newCss/blob/main/sticky.html)

# 끝
