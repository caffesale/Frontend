# DOM이란?

Document Object Model의 약자로 HTML, XML문서의 프로그래밍 인터페이스다. DOM은node와 objects를 이용해 문서를 표현하며 자바스크립트가 웹 문서에 접근할 수 있는 방법을 제공하여 문서 구조, 스타일, 내용을 변경할 수 있게 돕는다. 

# ReactDOM

자바스크립트에서 querySelector, getElementById등을 통해 DOM객체를 조작할 수 있지만 규모가 커질수록 DOM 트리에 접근하는 비용이 커진다.
React에서는 이 비용을 줄이기 위해 가상DOM에 해당하는 ReactDom을 활용한다. ReactDom은 React 특유의 LifeCycle에 따라 렌더링되는데 처음 렌더링 될 때와 컴포넌트에 변동사항이 있을 때 변경점이 있는 ReactDom을 실제 DOM에 일치시키는 방법으로 DOM 트리를 관리한다.
이를 통해 불필요한 렌더링 횟수를 줄일 수 있는 것이다.

# ShodowDOM?

HTML에서 video등의 태그를 사용했을 때 우리가 코딩하지 않은 재생, 일시정지, 볼륨등의 버튼이 이미 존재한다. 이것들은 숨겨진 DOM의 서브트리에 만들어진 것으로 브라우저에 의해 만들어진 것이다. 
ShodowDOM에 감춰진 요소들은 일반적인 CSS, 자바스크립트의 DOM조작에 영향을 받지 않는다. 
