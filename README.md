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

- [지원 브라우저-scroll-snap-type](https://caniuse.com/?search=scroll-snap-type), [지원 브라우저-scroll-snap-type](https://caniuse.com/?search=scroll-snap-align)
- [테스트 코드](https://github.com/leeseungje/newCss/blob/main/scroll-snap.html)

## :is pseudo selector
- 편의한 다수 선택자

## flex box gap
- flex layout 간격을 margin이 아닌 gap 프로퍼티를 주는 기능

## aspect-ratio
- 사이트에서 영상 혹은 이미지를 보여줄때 정해진 비율을 유지하고 싶을때 쓰는 기능

## :sticky
- 해당 엘레먼트를 사용하면 정의된 높이의 부모 div에 고정이 되는 기능
