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

## :is pseudo selector
- 편의한 다수 선택자

## flex box gap
- flex layout 간격을 margin이 아닌 gap 프로퍼티를 주는 기능

## aspect-ratio
- 사이트에서 영상 혹은 이미지를 보여줄때 정해진 비율을 유지하고 싶을때 쓰는 기능

## :sticky
- 해당 엘레먼트를 사용하면 정의된 높이의 부모 div에 고정이 되는 기능
