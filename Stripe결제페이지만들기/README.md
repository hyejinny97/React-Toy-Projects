# ✔ Stripe 결제 페이지 만들기

-   개요: Stripe 사의 랜딩 페이지 만들기
-   주요 개념: `useState()`, `useEffect()`, `useContext()`, `useRef()`, `react-icons`

## 🎨 FlowChart & Structure

### ▶ FlowChart

![](image/flowchart.PNG)

### ▶ Structure

![](image/structure.PNG)

## 🧩 실습 결과물

-   사이트 링크: <https://g2gtb7.csb.app/>
-   CodeSandbox 링크: <https://codesandbox.io/s/stripe-g2gtb7>

![](../gif/stripe_practice1.gif)

## 💡 후기

### ▶ 튜토리얼 vs 나의 코드

> 튜토리얼

-   context API를 사용해 여러 components에서 사용되는 'state'와 state를 변경하는 'handler function'을 공유하였음

    -   context에 의해 공유되는 values: `isSidebarOpen` state, `openSidebar` handler, `closeSidebar` handler, `isSubmenuOpen` state, `openSubmenu` handler, `closeSubmenu` handler, `page` state, `location` state

-   Navbar component

    -   mouseover event를 navbar 전체에서 watch하게 한 후, menu 버튼에 발생된 event가 아닌 경우에 `closeSubmenu` handler를 호출했음
    -   menu 버튼에 또 다른 mouseover event를 달아놓은 후, event가 발생하면 `openSubmenu` handler를 호출해 'page' 값과 버튼의 중심아래위치를 담은 'location' 값을 넘겨줬음

-   Submenu component

    -   context로부터 `isSubmenuOpen`, `page`, `location` state를 받음
    -   useEffect 훅을 사용해 Submenu component가 처음 render될 때, style을 변경해 화면 상에서의 submenu 위치를 결졍해줌
    -   또한, useEffect 훅에서 columns state를 변경해 links 개수에 따라 link 배치를 다르게 설정하였음
    -   `isSubmenuOpen`이 true일 때만 submenu component를 화면에 나타나게 함

-   Sidebar component

    -   context로부터 `isSidebarOpen` state, `closeSidebar` handler를 받음
    -   `isSidebarOpen`이 true일 때만 sidebar component를 화면에 나타나게 함

-   Hero component
    -   context로부터 `closeSubmenu` handler를 받아, banner 위에 mouseover되면 호출함
    -   hero 요소를 'height: 100vh'로 잡은 후, navbar의 높이만큼 'margin-top: -5rem'으로 올려 navbar와 hero를 겹치게 구현했음
    -   hero 요소의 '::before'를 hero 요소와 동일 위치.크기로 둔 후, 'background: url(hero.svg)'를 넣고 'z-index: -1'로 두어 배경을 만들어줬음

> 나의 코드

-   Redux Store를 사용해 state를 저장함

    -   store = {sidebar: {isOpened: bool}}
    -   action creator functions: `open`, `close`

-   GNB component

    -   GNB 각 menu 내 LNB를 같이 두고, 처음엔 'display: none'으로 두어 화면에서 보이지 않게 했다가 hover될 경우 'display: block'으로 스타일링 변화를 주어 화면에 보이게 했음
    -   burger button을 클릭할 경우, open action type으로 dispatch를 보내 Redux Store에 있는 sidebar isOpened를 true로 변경해줌

-   LNB component

    -   LMB component는 GNB component의 하위에만 존재해 각 submenu에 대한 정보를 넘겨받음
    -   튜토리얼처럼 `isSubmenuOpen`, `location` state를 받지 않고 전부 css로 처리함

-   SideBar component

    -   Redux Store 내 sidebar isOpened state가 true인 경우 화면에 나타나게 함
    -   close button을 클릭할 경우, close action type으로 dispatch를 보내 Redux Store에 있는 sidebar isOpened를 false로 변경해줌
    -   useEffect 훅을 통해 브라우저 창의 크기가 576px 이상이 되면 isOpened를 false로 변경해줘 자동으로 sidebar가 화면에서 보이지 않게 처리함

-   HeroBanner component
    -   GNB와 Hero를 겹치게 두기 위해 둘의 상위 component인 App을 'position: relative'로 두고, GNB와 Hero를 모두 'position: absolute'로 둔 후 'top: 0'으로 일치시켰음
    -   'banner.svg'는 img tag에 넣어 배경을 설정해줬음
    -   이 부분은 튜토리얼처럼 간단하게 css를 통해 구현하는 방법이 더 괜찮은 방법인 것 같음
