## 상태관리를 왜 할까요? 그리고 평소 state 관리는 어떻게 하시나요?

+ **상태 란?**
    + React에서 State는 component 안에서 관리되고 사용자의 액션에 따라 변경될 수 있는 JS객체이다.
    
+ **state는 특징으로**
    + 자식 컴포넌트간의 다이렉트 데이터 전달은 불가능하다.
    + 자식 컴포넌트 간의 데이터를 주고 받기 위해서는 부모 컴포넌트가 필요하다.
    + 자식이 많아진다면 상태 관리가 매우 복잡해진다. > Props drilling 이슈 발생
+ **상태관리는 왜 해야하는가?**
    + 상태 관리의 복잡성을 해결하기 위해서이다. 예를 들어 A컴포넌트의 상태를 D컴포넌트에서 사용한다면 B,C는 필요하지 않지만 전달위해 Props를 만들어 넘겨주어야하는 문제가 있다. > Props drilling 이슈 발생
  
+ **평소 state 관리는 어떻게 하시나요?**
    + 평소 State 관리 방법으로는 전역을 관리할 state가 아닐 경우에는 react-hooks 인 useState를 주로 사용하였다. props로 값을 전달하여 공통으로 사용할 수 있었다.
