# ✔ Color Generator 만들기

-   개요: 컬러 제너레이터 만들기
-   주요 개념: `useState()`, `useEffect()`, `setTimeout()`, `clearTimeout()`, `try...catch문`, `event.preventDefault()`

## 🎨 FlowChart & Structure

### ▶ FlowChart

![](image/flowchart.PNG)

### ▶ Structure

![](image/structure.PNG)

## 🧩 실습 결과물

-   사이트 링크: <https://eux6ty.csb.app/>
-   CodeSandbox 링크: <https://codesandbox.io/s/color-generator-eux6ty>

![](../gif/ColorGenerator_practice1.gif)

## 💡 후기

### ▶ 튜토리얼 vs 나의 코드

> 튜토리얼

-   입력란에 color 입력 후 제출 시, `values.js` 라이브러리의 Values 객체를 사용해 validation했음
    -   입력된 color가 invalid한 경우에는 error를 던지게 되고, try ~ catch문을 이용해 error를 잡아 error state를 true로 변경시켜 줌
    -   입력된 color가 valid한 경우에는 list state에 `Values(color).all(10)` 결과를 넣어준 후, SingleColor component에 각 Value를 prop으로 넘겨줌

> 나의 코드

-   입력란에 color 입력 후 제출 시, 정규표현식을 사용해 직접 validation을 진행하였음
    -   입력된 color가 invalid한 경우에는 invalid state를 true로 변경시켜 줌
    -   입력된 color가 valid한 경우에는 `showBoxes` state를 true로 변경시켜주게 되고, ColorBoxes component에 color state가 넘어가게 됨
-   ColorBoxes component는 각 Value를 ColorBox component에 prop으로 넘겨줌
