# OSS Week 12 — React Hooks Playground (Student Starter)

### Project Structure: App.jsx와 주요 Lab 컴포넌트의 역할
우선 프로젝트는 index.html → main.jsx → App.jsx → Lab 컴포넌트들의 순서로 연결된다. index.html은 React 앱이 실행되는 기본 HTML 파일이고, main.jsx는 App.jsx를 불러와 화면에 렌더링하는 역할을 한다. App.jsx에서는 useState를 이용해 현재 선택된 Lab을 관리하며, 버튼을 누르면 해당 Lab이 화면에 나타나는 것이다. Lab은 총 4개로 구성되어 있다. Lab 1은 useEffect를 이용한 타이머, Lab 2는 타이머의 시작과 정지 등을 하고, Lab 3은 useRef를 사용했고 입력창 관련된 것을 담당한다. 마지막으로 Lab 4는 useRef를 이용해서 타이머를 관리한다.

### useEffect: Effect, Dependency Array 및 Cleanup의 동작 원리
useEffect는 컴포넌트가 렌더링된 후 특정 작업을 실행할 때 사용하는 Hook이다. 이번 과제에서는 타이머를 실행하는 데 사용한다. Effect는 useEffect 안에 작성된 작업을 실행하는 것이고, Dependency Array는 Effect가 언제 다시 실행될지를 결정한다. 빈 배열 []을 넣으면 처음 마운트될 때 실행되기도 하고 running 값이 변경될 때마다 다시 실행하기도 한다. 배열을 생략하면 렌더링될 때마다 실행된다. Cleanup은 이전에 실행된 작업을 정리하는 역할을 하는데 이번 과제에서는 clearInterval을 통해 타이머가 계속 실행되지 않도록 한다.

### useRef: .current 속성과 useState의 차이
useRef는 값을 저장하거나 HTML 요소에 직접 접근할 때 사용하는 Hook이다. .current 속성을 통해 저장된 값에 접근하거나 변경할 수 있다. useState와의 가장 큰 차이점은 값이 변경되었을 때 렌더링이 발생하는지 여부이다. useState는 값이 변경되면 컴포넌트가 다시 렌더링되지만, useRef는 .current 값이 변경되어도 다시 렌더링되지 않는다.

### Code Analysis: useEffect와 useRef 관련 주요 코드 각 1개(5~15줄)를 선택하여 동작 원리 설명
- useEffect
Lab1에서는 useEffect를 이용해 1초마다 count가 증가하도록 한다. 먼저 setInterval을 통해 타이머를 생성하고, 생성된 타이머 ID를 timerId에 저장한다. 이후 setCount(prev => prev + 1)을 이용해 1초마다 count를 1씩 증가시키는 것이다. Dependency Array가 빈 배열이기 때문에 처음에 마운트될 때는 Effect가 실행되고, Cleanup에서는 clearInterval을 이용해 타이머가 정리된다. 이를 통해 useEffect가 실행되는 시점과 Cleanup의 역할을 확인할 수 있다.
- useRef
Lab4에서는 useRef를 이용해 타이머 ID를 저장하고 관리한다. 먼저 useRef(null)을 통해 timerRef를 생성한다. Start 버튼을 누르면 setInterval을 통해 타이머가 실행되고, 생성된 ID는 timerRef.current에 저장된다. 이때 이미 타이머가 실행 중이라면 중복 실행되지 않도록 한다. Stop 버튼을 누르면 clearInterval을 통해 타이머를 정지하고, timerRef.current를 null로 변경한다. 여기서 useRef는 값이 변경되어도 렌더링되지 않지만, useState로 관리하는 running은 값이 변경되면 화면에 반영된다. 이를 통해 useRef와 useState의 차이를 확인할 수 있다.

# Lab 비교 분석
### useEffect의 Dependency Array가 필요한 이유는?
Dependency Array는 useEffect가 언제 다시 실행될지 정하기 위해 필요하다. 빈 배열 []을 사용하면 처음 마운트할 때 Effect가 실행되고, running도하면 running 값이 변경될 때마다 다시 실행되는 것이다. 근데 이때 Dependency Array를 빼게 되면 렌더링될 때마다 Effect가 실행되게 된다. 즉, 원하는 시점에만 실행되도록 할 수 있는 것이다.
### Cleanup을 사용하지 않으면 어떤 문제가 발생할 수 있는가?
Cleanup을 사용하지 않으면 전에 실행했던 작업이 남아있어 문제가 될 수 있다. 
예를 들면 Lab1에서 clearInterval을 사용하지 않으면 컴포넌트가 사라진 이후에도 타이머가 계속 진행 될 수 있다. 
그리고 또 Effect가 다시 실행될 때 기존 타이머가 남아있으면 여러 타이머가 중복으로 실행되는 문제가 생길 수 있다.
### useState와 useRef의 가장 중요한 차이는?
useState는 값이 바뀌면 컴포넌트가 다시 렌더링되어 화면에도 반영된다. 하지만 useRef는 .current에 저장된 값이 바뀌어도 랜더링되지 않는다. 그래서 화면에 표시해야 하는 것은 useState를, 화면을 다시 렌더링할 필요가 없는 것은 useRef를 사용하는 것이다.
### LAB 2와 LAB 4의 Timer 관리 방식은 어떻게 다른가?
모두 타이머를 시작, 멈춤, 초기화 할 수 있지만 타이머를 관리하는 부분에서 차이가 있다. Lab2에서는 running이 true로 바뀌면 Effect에서 타이머를 실행하고, false로 바뀌면 Cleanup을 통해 타이머를 정리하는 방식이다. Lab4는 Start 버튼을 누르면 타이머를 생성하고, Stop 버튼을 누르면 저장된 ID를 이용해서 타이머를 멈춘다. 즉, Lab2는 useEffect와 State의 변화에 따라 타이머를 바뀌게 하고, Lab4는 useRef를 이용해 타이머를 관리한다.

# Customizing
1. 제목변경
- 변경전 : React Hooks Playground
- 변경후 : 오소스 12주차 과제
2. CSS 스타일 2곳 이상 변경
- 변경전 : x
- 변경후 : background-color: khaki;
- 변경전 : background : white;
- 변경후 : background : green;
3. 4개 Lab 정상 동작 확인
확인!
4. Browser Console 오류 확인
확인!










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
