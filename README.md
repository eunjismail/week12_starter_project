# OSS Week 12 — React Hooks Playground (Student Starter)

# Project Structure: App.jsx와 주요 Lab 컴포넌트의 역할
우선 프로젝트는 index.html → main.jsx → App.jsx → Lab 컴포넌트들의 순서로 연결된다. index.html은 React 앱이 실행되는 기본 HTML 파일이고, main.jsx는 App.jsx를 불러와 화면에 렌더링하는 역할을 한다. App.jsx에서는 useState를 이용해 현재 선택된 Lab을 관리하며, 버튼을 누르면 해당 Lab이 화면에 나타나는 것이다. Lab은 총 4개로 구성되어 있다. Lab 1은 useEffect를 이용한 타이머, Lab 2는 타이머의 시작과 정지 등을 하고, Lab 3은 useRef를 사용했고 입력창 관련된 것을 담당한다. 마지막으로 Lab 4는 useRef를 이용해서 타이머를 관리한다.

# useEffect: Effect, Dependency Array 및 Cleanup의 동작 원리
useEffect는 컴포넌트가 렌더링된 후 특정 작업을 실행할 때 사용하는 Hook이다. 이번 과제에서는 타이머를 실행하는 데 사용한다. Effect는 useEffect 안에 작성된 작업을 실행하는 것이고, Dependency Array는 Effect가 언제 다시 실행될지를 결정한다. 빈 배열 []을 넣으면 처음 마운트될 때 실행되기도 하고 running 값이 변경될 때마다 다시 실행하기도 한다. 배열을 생략하면 렌더링될 때마다 실행된다. Cleanup은 이전에 실행된 작업을 정리하는 역할을 하는데 이번 과제에서는 clearInterval을 통해 타이머가 계속 실행되지 않도록 한다.

# useRef: .current 속성과 useState의 차이
useRef는 값을 저장하거나 HTML 요소에 직접 접근할 때 사용하는 Hook이다. .current 속성을 통해 저장된 값에 접근하거나 변경할 수 있다. useState와의 가장 큰 차이점은 값이 변경되었을 때 렌더링이 발생하는지 여부이다. useState는 값이 변경되면 컴포넌트가 다시 렌더링되지만, useRef는 .current 값이 변경되어도 다시 렌더링되지 않는다.







## 실행 방법
Node.js 20.19+ 또는 22.12+ 권장. 프로젝트 폴더에서 실행:

```bash
npm install
npm run dev   
```

브라우저에 터미널의 Local URL을 열고 LAB 탭을 이동하세요. 제출 전 `npm run build`도 실행하세요.

## 수행 방법
1. `src/components/` 아래의 LAB 1~4 파일에 있는 `TODO`를 직접 완성합니다.
2. `src/App.jsx`, `src/App.css`는 공통 화면이므로 가급적 수정하지 않습니다.
3. 각 LAB의 동작 화면과 콘솔 결과를 기록합니다.
4. 한 LAB에서 다른 LAB으로 탭을 전환하면 기존 컴포넌트가 언마운트됩니다. Cleanup 결과를 관찰합니다.


## 이해도 확인 질문
1. `setCount(prev => prev + 1)`은 왜 유용한가?
2. `useEffect(fn, [])`과 `useEffect(fn)`은 어떻게 다른가?
3. Cleanup은 언제 실행되는가? 개발 환경 StrictMode 영향은?
4. `useState`와 `useRef`의 값 변경 시 렌더링 차이는?
5. LAB 2와 LAB 4에서 Timer를 관리하는 방식의 차이는?
