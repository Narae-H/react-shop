# React 란? :camera_flash:
Single Page Application으로 새로고침 없이 부드럽게 이동 가능한데 그 이유는
- html 파일을 1개만 쓰고
- 다른 페이지 보여주고 싶을때는 html 부분만 바꿔주기 때문

### 사용이유
- JavaScript로 생짜코딩 가능하나 길어지니깐 **리액트라는 자바스크립트 라이브러리** 이용
- html을 **함수, array, object** 이런 곳에 보관하고 재사용

### 설치 및 개발환경 셋팅
1. [Node.js 웹사이트](https://nodejs.org/en) 에서 LTS라고 써있는 버전 설치 *chocolatey 설치 안해도 됨.
2. VS Code 설치
3. 작업용 폴더 생성
4. 폴더에서 Shift + 우클릭해서 'Open powershell window here' 선택
5. 터미널에서 명령어 입력해서 프로젝트 생성
```shell
npx create-react-app [프로젝트명]
```
7. VS code > Open folder > 생성된 프로젝트명 선택
8. Terminal > New Terminal
9. 터미널에 **npm start** 입력(내 사이트를 브라우저로 미리보기 띄우기)

> [!NOTE]
> <details>
> <summary> 참고: JSX</summary>
> React의 js파일에서 쓰는 HTML
>
> ### 주요문법
> 1) className   : HTML 태그 내에서 classs는 className으로 쓴다. => class는 js에서 예약어이므로.
> 2) 데이터 바인딩: HTML 안에서 데이터를 바인딩 하고 싶을 때는 {중괄호} 를 쓴다.
> 3) style key값 : HTML 태그 내에서 style 작성 시 키 값이 '-'로 되있는 경우는 카멜표기법으로 쓴다 => js파일에서 '-'는 뺄셈을 뜻하므로.
> ```HTML
> <div className='black-nav'>
>   <p>{data}</p>
>   <p style={{color: 'red', fontSize: '16px'}}>style</p>
> </div>
> ```
> </details>

# state
### state란?
자료를 잠깐 보관하는 곳. state는 변동 사항이 생기면 자동으로 html을 재랜더링 해줌 => 즉, **자주 값이 자주 바뀌어서 재랜더링이 필요한 곳**에 쓰면 됨.
|      특징      |   state                              |  변수                                                |
|----------------|--------------------------------------|-----------------------------------------------------|
|     공통점     | 변수를 보관                            | 변수를 보관                                          |
|     차이점     | state에 저장된 값이 변경되면 HTML **자동으로 재렌더링 O** | 변수에 저장된 값이 변경되도 HTML **다시 랜더링 X** -> 새로 고침 필요|

### 문법
- **기본 사용법**   
**let[**_state이름, state변경 함수 이름으로 함수로 set[변수명]으로 작명_**]** = **useState(**_'state에 넣을 값'_**);**
```JavaScript
(App.js)

import {useState} from 'react';

function App() {
  let[postName1, setPostName1] = useState('여자코트 추천');                   // 변수에 단일 값을 넣는 경우
  let[postName2, setPostName2] = useState(['여자코트 추천', '남자코트 추천']); // 변수에 array type으로 값을 넣는 경우

  return (
    <div>
      <p>{postName1}</p>
      <p>{postName2[0]}</p>
      <p>{postName2[1]}</p>
    </div>
  )
}
```
> [!NOTE]
> <details>
> <summary>자바스크립트 destructuring 문법</summary>
>   
> ```JavaScript
> // array안의 데이터들을 하나 하나 변수에 바인딩  
> let array = ['Hyeon', 20];
> let name  = array[0];
> let age   = array[1];
> 
> // 위의 코드 대신에 아래와 같이 사용. 왼쪽 오른쪽 형식을 똑같이 맞추면 자동으로 알아서 변수 생성
> let [name, age] = ['Hyeon', 20]
> ```
> </details>

- **state 변경하는 법**    
state만 변경했다고 해서 값이 바로 변경되는 것이 아니라, state변경 함수를 이용하여 state값을 저장해야 HTML 재렌더링이루어짐.
```JavaScript
// 👍 눌렀을 때, likes가 1씩 증가하는 함수
function App(){
  let [likes, setLikes] = useState(0);
  
  return (
     <h4> 글 제목 <span onClick={ () => { setLikes(likes++) }} >👍</span> { likes }</h4>
  )
}
```
> [!NOTE]
> <details>
> <summary> JSX에서 onClick 함수 사용</summary>
>
> 1) onClick에서 'C'는 대문자로
> 2) onClick 다음에는 { } 중괄호 사용
> 3) { } 안에는 함수를 넣어야 함
> </details>

- **state 변경함수 특징**
1) **기존 state == 신규 state** 가 **true**라면 동작하지 않음
2) JavaScript는 **call by sharing** 특징을 가지고 있으므로, 원시타입은 새로운 저장소에 값이 복사되고 객체타입(array, object, function)은 새로운 저장소에 주소값이 복사됨
3) 때문에, **let copiedObj = [...originObj]** 와 같이 전개(...)연산자(speard operation)를 사용하여 []를 풀어서 원시타입으로 저장해야 state변경함수에서 값이 변경된 것을 인지하고 HTML 재렌더링 가능 

> [!NOTE]
> <details>
> <summary>...연산자 (speard operation)</summary>
>
> 괄호를 벗겨서 객체타입을 원시타입으로 바꾸기 위한 연산자
> ```JavaScript
> let data1 = [1, 2, 3];
> let data2 = ...data1;
> 
> console.log(data2)     // 결과값: 1, 2, 3
> ```
> </details>

> [!NOTE]
> <details>
> <summary> JavaScript의 call by sharing</summary>
>
> 객체타입은 새로운 저장소에 값이 복사되는게 아니라 주소값이 복사됨.
> ```JavaScript
> // 1. 얕은 복사 (shallow copy)
> let originObj  = [1, 2, 3];
> let sCopiedObj = originObj;
> console.log( originObj );                 // 결과값: [1, 2, 3]
> console.log( sCopiedObj );                // 결과값: [1, 2, 3]
> console.log( originObj == sCopiedObj );   // 결과값: true (originObj이 저장하고 있는 주소값과 sCopiedObj가 저장하고 있는 주소값이 동일)
> 
> // 2. 다른 객체에 같은 값 대입 
> let originObj2  = [1, 2, 3];
> let sCopiedObj2 = [1, 2, 3];
> console.log( originObj2 );                // 결과값: [1, 2, 3]
> console.log( sCopiedObj2 );               // 결과값: [1, 2, 3]
> console.log( originObj2 == sCopiedObj2 ); // 결과값: false (originObj이 저장하고 있는 주소값과 sCopiedObj가 저장하고 있는 주소값이 다름)
> 
> // 3. 복사된 객체에 새로운 값 추가
> sCopiedObj.push(4);                       // sCopiedObj에만 값을 추가. 정확히는 sCopiedObj가 저장하고 있는 주소값에 가서 객체 변경 
> console.log( originObj );                 // 결과값: [1, 2, 3, 4]
> console.log( sCopiedObj );                // 결과값: [1, 2, 3, 4]
> console.log( originObj == sCopiedObj );   // 결과값: true (originObj이 저장하고 있는 주소값과 sCopiedObj가 저장하고 있는 주소값이 동일) 
> 
> // 4. 깊은 복사 (deep copy)
> let dCopiedObj = [...originObj];          // 전개(...) 연산자를 사용하여 복사된 값을 새로운 주소에 저장. 하지만 전개 연산자도 depth-level1까지만 복사 가능
>                                           // 참고: depth-level2에 또 다시 객체가 나온다면 다시 주소 값을 복사하여 저장하게 됨 
> dCopiedObj.push(5);
> console.log( originObj );                 // 결과값: [1, 2, 3, 4]
> console.log( dCopiedObj );                // 결과값: [1, 2, 3, 4, 5]
> console.log( originObj == dCopiedObj );   // 결과값: false (originObj이 저장하고 있는 주소값과 sCopiedObj가 저장하고 있는 주소값이 다름) 
> 
> // 5. 완전 깊은 복사
> // 1) 모든 깊이의 객체까지 복사하는, 커스텀 재귀 함수 사용
> // 2) Lodash의 cloneDeep() 사용 (별도 패키지 설치)
> // 3) JSON 객체의 메소드 이용 JSON.stringfy, JSON.parse
> ```
> </details>

# Component
### Component란?
많은 HTML tag들을 한 단어로 줄이고 싶을 때 사용 => 즉, **반복적인 html 축약/큰 페이지 저장/내용이 매우 자주 변경되는 HTML 사용**하면 됨

### 문법
Step 1) function 만듬 (function 이름은 첫글자는 대문자로)    
Step 2) 그 함수의 return 안에 축약하고 싶은 html 담기    
Step 3) 원하는 곳에 <함수명/> 사용하면 축약한 html 나옴    
```JavaScript
function App (){
  return (
    <div>
      (생략)
      <Modal/>
    </div>
  )
}

function Modal () {
  return (
    <div className="modal">
      <h4>제목</h4>
      <p>날짜</p>
      <p>상세내용</p>
    </div>
  )
}
```

### 동적인 UI로 활용
Step 1) html css로 미리 UI 디자인    
Step 2) UI의 현재 상태를 state로 저장    
Step 3) state에 따라서 UI가 어떻게 보일지 조건문 등으로 작성    
```JavaScript
function App (){
  let [modalState, setModalState] = useState(0);

  return (
    <div>
      (생략)
      <button onClick={ () => { setModalState(1) }}>모달 보여줘</button>
      {
        modalState? <Modal/> : null
      }
    </div>
  )
}

function Modal () {
  return (
    <div className="modal">
      <h4>제목</h4>
      <p>날짜</p>
      <p>상세내용</p>
    </div>
  )
}
```
> [!NOTE]
> <details>
> <summary>JSX의 조건문</summary>
>
> JSX 안에서는 if/else 문법을 바로 사용할 수 없음. 대신에 삼항연산자를 { }에서 사용가능
> ```JavaScript
> { 2 > 1 ? console.log('맞음): console.log('틀림') }
> ```
> </details>

> [!NOTE]
> <details>
> <summary>[].module.css 파일</summary>
>
> CSS파일 만들 때, 여러군데에서 겹치는 걸 막기위해서 하나의 js파일에만 종속적인 파일 만들 수 있음
> 이름을 **App.module.css**와 같이 만들면, App.js에서만 종속되는 파일 생성 가능.
> </details>

# Props


# Hook
###  Hook 이란?
Hook은 16.8에서 새롭게 도입된 기능으로 함수형 컴포넌트에서 React state와 생명주기 기능을 연동할 수 있게 해주는 함수.
내장훅(use로 시작하는 함수)과 custom hooks가 있음 ex) useState(), useEffect()

### Hook 사용 이유
컴포너트 간의 계층을 바꾸지 않고 상태 로직을 재사용 할 수 있음.
하나의 컴포넌트 생명주기가 아닌 기능을 기반으로 하여 작은 함수 단위로 나눌 수 있음.

### Hook 규칙/문법
1) 같은 hook을 여러 번 호출 가능
```JavaScript
function App() {
  let [name, setName] = useState('홍길동');
  let [age, setAge]   = useState(20); 
}
2) 최상위 component에서만 호출 가능, 반복문/조건문/중첩된 함수 내에서 호출하면 안됨
```JavaScript
// 좋은 예
function MyComponent () {
  let [test, setTest] = useState(123);
  if ( [조건] ) {
    [생략]
  }
}

// 나쁜 예
function MyComponent () {
  if( [조건]) {
    let [test, setTest] = useState(123);
  }
}
```
3) 비동기함수 (async 키워드 붙은 함수)는 콜백함수로 사용할 수 없음
```JavaScript
function App() {
  useEffect(async () => {     // 에러 발생: Hook 함수 내에 비동기 함수 쓰였으므로. 
    await Promise.resolve(1); 
  })
}
``` 


# Import/Export

# Route

# UseNavigate

# Lifecycle
### Lifecycle이란?
React에서 'mount(페이지 최초로 로딩), update (HTML재랜더링), unmount (다른페이지로 이동)' 3개의 사이클 단계를 거치는데, 특정 단계에서 특정 코드 사용가능.
그럼 언제 사용할까? => 특정 lifecycle 단계에서 실행하고 싶을 때

### 문법
useEffect()를 사용하여 react의 lifecycle의 특정 단계에서 관여 가능하며, useEffect()는 component 내의 상태 변화(side effect: 의도하지 않은 결과)가 있을 때 이를 감지하여 특정작업을 해줄 수 있는 훅
```JavaScript
function App() {
  // useEffect() 안에 쓴 코드는 HTML이 전부 다 랜더링이 된 다음에 실행됨.
  // 크게 아래의 3가지 코드를 이곳에 사용
  // 1) 시간이 오래 걸리는 작업: JavaScript는 코드를 위에서 아래로 읽으므로 상단에 너무 시간이 오래 걸리는 작업이 있으면 HTML 랜더링이 안됨.
  // 2) 서버에서 데이터 가져오는 작업들: 데이터를 가져오기전에 HTML 랜더링 먼저되어도 상관없으므로
  // 3) 타이머 장착하는 것들

  // 1. useEffect()의 두번째 인자로 아무것도 전달안함: mount, update 단계에서 실행. 클래스 컴포넌트의 componentDidMount, componentDidUpdate 과 동일
  useEffect (() => { })

  // 2. useEffect()의 두번째 인자로 빈 배열 전달:  mount 단계에서 실행. 클래스 컴포넌트의 componentDidMount, componentDidUpdate 과 동일
  useEffect (() => { }, [])

  // 3. useEffect()의 두번째 인자로 변수 전달: mount와, 인자가 변경될 때(아래코드에서는 count) 실행
  useEffect (() => { }, [count])

  // 4. useEffect()의 첫번째 인자의 return: unmount 때 실행
  useEffect (() => { return '' // unmount 될 때 실행 }, [])

  return (
    [생략]
  )
}
```

# JavaScript참고 문법
1. map()
2. sort()
3. find()
