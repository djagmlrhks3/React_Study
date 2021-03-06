# React

## 1장

## Why React?

JS의 발전

과거)  웹 브라우저에서 간단한 연산을 하거나 시각저깅ㄴ 효과를 주는 단순한 스크립트 언어

현재) 웹 애플리케이션에서 가장 핵심적인 역할. 서버 사이드는 물론 모바일, 데스크톱 애플리케이션에서도 엄청난 활약중



JS(일렉트론 - 자바스크립트로 데스크톱 애플리케이션을 만들 수 있는 프레임워크)로 개발한 것

* Slack
* Atom
* VS Code

모바일 애플리케이션에서도 여러 프레임워크(React Native, Titanium, Ionic, NativeScript 등)를 사용하여 페이스북, 디스코드 페이팔, 이베이 등 수 많은 애플리케이션을 개발했다.



JS 기반의 프레임워크들(React, Vue, Angular 등)은 주로 MVC, MVVM 아키텍처를 사용한다. (Angular의 경우 MVW)

공통점은 모델(Model)과 뷰(View)가 있다.

* 모델(Model) : 애플리케이션에서 사용하는 데이터를 관리하는 영역
* 뷰(View) : 사용자에게 보여지는 부분

프로그램이 사용자에게서 어떤 작업을 받으면 컨트롤러는 모델 데이터를 조회하거나 수정하고, 변경된 사항을 뷰에 반영한다.

반영하는 과정에서 보통 뷰를 변형(mutate)한다.



소규모의 애플리케이션에서는 업데이트하려는 항목에 따라 어떤 부분을 찾아서 변경할지 규칙을 정하는 작업이 간단하지만, 애플리케이션 규모가 크면 상당히 복잡해지고 제대로 관리하지 않으면 성능이 떨어질 수 있다.

→ 페이스북 개발 팀이 이를 해결하고자 React를 개발

어떤 데이터가 변할 때마다 어떤 변화를 줄지 고민하는 것이 아니라 그냥 기존 뷰를 날려 버리고 처음부터 새로 렌더링하는 방식

장점

* 애플리케이션 구조가 매우 간단
* 작성해야 할 코드양이 많이 줄어든다.
* 더 이상 어떻게 변화를 줄지 신경 쓸 필요가 없고, 그저 뷰가 어떻게 생길지 선언하며, 데이터에 변화가 있으면 기존에 있던 것은 버리고 정해진 규칙에 따라 새로 랜더링하면 된다.

단점

* 개선된 방식으로 하면 CPU 점유율이 크게 증가한다.
* DOM이 느리기 때문에 메모리도 많이 사용하게 된다.
* 사용자가 인풋 박스에 텍스트를 입력할 때 기존에 렌더링된 것은 사라지고, 새로 랜더링하면 끊김 현상이 발생하게 된다.

## 리액트 이해

구조가 MVC, MVW 등인 프레임워크와 달리, 오직 V(View)만 신경 쓰는 라이브러리다.

컴포넌트 : 특정 부분이 어떻게 생길지 정하는 선언체

cf) 템플릿은 보통 데이터셋이 주어지면 HTML 태그 형식을 문자열로 반환

반면, 컴포넌트는 재사용이 가능한 API로 수많은 기능들을 내장하고 있으며, 컴포넌트 하나에서 해당 컴포넌트의 생김새와 작동 방식을 정의할 수 있다.



### 초기 랜더링

render() { ... } : 컴포넌트가 어떻게 생겼는지 정의하는 역할(함수)

이 함수는 html 형식의 문자열을 반환하지 않고, 뷰가 어떻게 생겼고 어떻게 작동하는지에 대하 정보를 지닌 객체를 반환한다.



컴포넌트 내부에는 또 다른 컴포넌트들이 들어갈 수 있다. 이 때 render 함수를 실해하면 그 내부에 있는 컴포넌트들도 재귀적으로 렌더링한다.

이렇게 최상위 컴포넌트의 렌더링 작업이 끝나면 지니고 있는 정보들을 사용하여 HTML 마크업을 만들고, 이를 우리가 정하는 실제 페이지의 DOM 요소 안에 주입한다.



### 조화 과정

리액트 라이브러리에서 업데이트를 진행하는 중요한 부분!

뷰를 업데이트할 때 "업데이트 과정을 거친다"라기보단 "조화 과정을 거친다"고 하는 것이 더 정확하다.

컴포넌트에서 데이터에 변화가 있을 때 우리가 보기에는 변화에 따라 뷰가 변형되는 것처럼 보이지만, 사실은 새로운 요소로 갈아 끼운다. → by render 함수

새로운 데이터를 가지고 render 함수를 또 다시 호출한다. 그러면 그 데이터를 지닌 뷰를 생성한다. 하지만 이때 render 함수가 반환하는 결과를 곧바로 DOM에 반영하지 않고, 이전에 render 함수가 만들었던 컴포넌트 정보와 현재 render 함수가 만든 컴포넌트 정보를 비교하여, 두 가지 뷰를 최소한의 연산으로 DOM 트리에 업데이트한다.

결국 방식 자체는 루트 노드부터 시작하여 전체 컴포넌트를 처음부터 다시 렌더링하는 것처럼 보이지만, 사실 최적의 자원을 사용하여 이를 수행하는 것!



## 리액트의 특징

### DOM이란?

Document Object Model

즉, 객체로 문서 구조를 표현하는 방법으로 XML이나 HTML로 작성

웹 브라우저는 DOM을 활용하여 객체에 JS와 CSS를 적용한다. DOM은 트리 형태라서 특정 노드를 찾거나 수정하거나 제거하거나 원하는 곳에 삽입할 수 있다.



DOM의 치명적인 한 가지 문제점은 동적 UI에 최적화되어 있지 않다는 것이다.

HTML은 자체적으로 정적이다. 하지만 JS를 사용하여 이를 동적으로 만들 수 있다.



DOM 자체는 빠르다. 단, 웹 브라우저 단에서 DOM에 변화가 일어나면 웹 브라우저가 CSS를 다시 연산하고, 레이아웃을 구성하고, 페이지를 리페인트한다. 이 과정에서 많은 시간이 허비된다.

→ 해결법 : HTML 마크업을 시각적인 형태로 변환하는 것은 웹 브라우저가 하는 주 역할이다. 이를 처리할 때 컴퓨터 자원을 사용하는 것은 어쩔 수 없다. 하지만 DOM을 조작할 때마다 엔진이 웹 페이지를 새로 그리므로 잦은 업데이트는 성능이 저하된다. 따라서 DOM을 최소한으로 조작하여 작업을 처리하는 방식으로 개선할 수 있다.

리액트는 Virtual DOM 방식을 사용하여 DOM 업데이트를 추상화함으로써 DOM 처리 횟수를 최소화하고 효율적으로 진행한다.



### Virtual DOM

Virtual DOM을 사용하면 실제 DOM에 접근하여 조작하는 대신, 이를 추상화한 JS 객체를 구성하여 사용한다. (마치, 실제 DOM의 가벼운 사본)

react에서 DOM을 업데이트할 때 3가지 절차

1. 데이터를 업데이트하면 전체 UI를 Virtual DOM에 리랜더링한다.
2. 이전 Virtual DOM에 있던 내용과 현재 내용을 비교한다.
3. 바뀐 부분만 실제 DOM에 적용한다.

※ 오해

Virtual DOM 사용은 사용하지 않을 때와 비교하여 무조건 빠르다? → No

ex) 단순 라우팅 정도만 있는 정적인 페이지에서는 오히려 사용하지 않는 편이 더 나은 성능을 보이기도 한다.



### 기타 특징

리액트는 프레임워크가 아니라 라이브러리다.

다른 웹 프레임워크가 Ajax, 데이터 모델링, 라우팅 등과 같은 기능을 내장하고 있는 반면, 리액트는 정말 뷰만 신경 쓰는 라이브러리다. (따라서, 기타 기능은 직접 구현하여 사용해야 한다.)

※ 기타 기능 - 라이브러리 사용

* Ajax 처리에는 axios나 fetch
* 상태 관리에는 리덕스(redux)나 MobX

장점) 해당 분야에서 마음에 드는 라이브러리를 사용하면 되니까 자신이 취향대로 스택을 설정할 수 있다. 또한 다른 웹 프레임워크나 라이브러리와 혼용할 수 있다.

단점) 여러 라이브러리를 접해야 한다.



## 작업 환경 설정

### Node.js와 npm

Node.js

크롬 V8 자바스크립트 엔진으로 빌드한 JS 런타임이다.

Node.js로 웹 브라우저 환경이 아닌 곳에서도 JS를 사용하여 연산할 수 있다.

2009년 출시한 이후 JS는 웹 브라우저 영역 외에 웹 서버, 모바일 애플리케이션, 데스크톱 애프리케이션 영역에서도 엄청난 활약을 하게 된다.



리액트 애플리케이션은 웹 브라우저에서 실행되는 코드이므로 Node.js와 직접적인 연관은 없지만, 프로젝트를 개발하는 데 필요한 주요 도구들이 Node.js를 사용하기 때문에 설치해야 한다.

사용하는 개발도구

* ECMAScript 6를 호환시켜주는 **바벨(babel)**
* 모듈화된 코드를 한 파일로 합치고(번들링) 코드를 수정할 때마다 웹 브라우저를 리로딩하는 등의 여러 기능을 지닌 **웹팩(webpack)** 등이 있다.

npm

* Node.js 패키지 매니저 도구
* npm으로 수 많은 개발자가 만든 패키지(재사용이 가능한 코드)를 설치하고 설치한 패키지의 버전을 관리할 수 있다. (리액트 역시 하나의 패키지다.)



### yarn

Node.js를 설치할 때, 패키지를 관리해 주는 npm이라는 도구가 설치된다.

하지만 npm 대신 yarn이라는 패키지 관리자 도구를 설치하여 사용할 것이다.

yarn은 npm을 대체할 수 있는 도구로 npm보다 더 빠르며 효율적인 캐시 시스템과 기타 부가 기능을 제공한다.

```cmd
npm install --global yarn
```



### 에디터 설치

VS Code : 모든 운영체제를 지원하는 에디터 (made by MS)

유용한 익스텐션

* ESLint : JS 문법 및 코드 스타일을 검사
* Reactjs Code Snippets : 리액트 컴포넌트 및 라이프사이클 함수를 작성할 때 단축 단어를 사용하여 간편하게 코드를 자동으로 생성해 낼 수 있는 스니펫 모음 (by charalampos karypidis)
* Prettier-Code formatter : 코드 스타일을 자동으로 정리해 주는 도구



### create-react-app으로 프로젝트 생성

```cmd
# yarn 사용시
yarn create react-app <프로젝트 이름>
cd <프로젝트 이름>
yarn start

# yarn 미사용시
npm init react-app <프로젝트 이름>
```



yarn 권한 설정 이슈 : https://singa-korean.tistory.com/21



## 2장

## 코드 이해하기

> src/App.js

node_modules 디렉터리에 react 모듈이 설치된다. 그리고 import 구문을 통해 리액트를 불러와서 사용할 수 있다.

모듈을 불러와서 사용하는 것은 사실 원래 브라우저에 없던 기능이다. 브라우저가 아닌 환경에서 JS를 실행할 수 있게 해주는 환경인 Node.js에서 지원하는 기능이다.

참고) Node.js에서는 import가 아닌 require라는 구문으로 패키지를 불러온다.

이러한 기능을 브라우저에서도 사용하기 위해 번들러(bundler)를 사용한다. 번들(bundle)은 묶는다는 뜻이다. 즉, 파일을 묶듯이 연결한다. 대표적인 번들러로 웹팩, Parcel, browserify라는 도구들이 있으며, 각 도구마다 특성이 다르다.

리액트 프로젝트에서는 주로 웹팩을 사용한다.

```react
import logo from './logo.svg';
import './App.css';
```

웹팩을 사용하면 SVG파일과 CSS파일도 불러와서 사용할 수 있다.

이렇게 파일들을 불러오는 것은 웹팩의 로더(loader)라는 기능이 담당한다.

로더는 여러 가지 종류가 있다.

* css-loader : CSS 파일을 불러올 수 있게 해준다.
* file-loader : 웹 폰트나 미디어 파일 등을 불러올 수 있게 해준다.
* babel-loader : JS 파일들을 불러오면서 최신 JS 문법으로 작성도니 코드를 바벨이라는 도구를 사용하여 ES5 문법으로 변환해 준다.(호환을 위해)



## JSX란?

자바스크립트의 확장 문법이다. (XML과 매우 비슷하게 생겼다.)

브라우저에서 실행되기 전에 코드가 번들링되는 과정에서 바벨을 사용하여 일반 JS 형태의 코드로 변환한다.

JSX를 사용하면 매우 편하게 UI를 렌더링할 수 있다.

JSX는 공식적인 JS 문법이 아니다. 바벨을 통해 개발자들이 임의로 만든 문법, 혹은 차기 JS 문법들을 사용할 수 있다.



## JSX의 장점

### 보기 쉽고 익숙하다

가독성이 높고 작성하기 쉽다.



### 더욱 높은 활용도



## JSX 문법

JSX는 편리한 문법이지만, 올바른 사용을 위해 준수해야 할 규칙이 있다.



### 감싸인 요소

컴포넌트에 여러 요소가 있다면 반드시 부모 요소 하나로 감싸야 한다.

이유 : Virtual DOM에서 컴포넌트 변화를 감지해 낼 때 효율적으로 비교할 수 있도록 컴포넌트 내부는 하나의 DOM 트리 구조로 이루어져야 한다는 규칙이 있다.

```react
import React from 'react';

function App() {
    return (
      <div>  // div로 감싸야 한다.
    	<h1>Hi React!</h1>
        <h2>Hello!</h2>
      </div>
    )
}
```



리액트 v16 이상부터는 Fragment 기능을 사용할 수 있다.

```react
import React from 'react';

function App() {
    return (
      <Fragment>  // div로 감싸야 한다.
    	<h1>Hi React!</h1>
        <h2>Hello!</h2>
      </Fragment>
    )
}
```

또는 아래와 같은 형태로도 표현할 수 있다.

```react
import React, { Fragment } from 'react';

function App() {
    return (
      <>  {/* div로 감싸야 한다. */} 
    	<h1>Hi React!</h1>
        <h2>Hello!</h2>
      </>
    )
}
```



### 자바스크립트 표현

JSX는 DOM 요소를 렌더링하는 기능외에도 JSX내부에 JS 표현식을 쓸 수 있다.

JSX내부에서 코드를 `{ }`로 감싸면 된다.

```react
import React, { Fragment } from 'react';

function App() {
    const name = 'React';
    return (
      <Fragment>
    	<h1>Hi { name }!</h1>
        <h2>Hello!</h2>
      </Fragment>
    )
}
```



### If 문 대신 조건부 연산자

JSX 내부의 JS 표현식에서 if 문을 사용할 수는 없다.

하지만 조건에 따라 다른 내용을 렌더링해야 할 때는 JSX 밖에서 if 문을 사용하여 사전에 값을 설정하거나, { } 안에 조건부 연산자를 사용하면 된다.

조건부 연산자의 또 다른 이름은 삼항 연산자!

```react
import React from 'react';

function App() {
  const name = 'React';
  return (
    <div className="App">
      {name === 'React' ? (
        <h1>Hi {name}!</h1>
      ) : (
        <h1>Not React</h1>
      )}
      <h2>Hello!</h2>
    </div>
  );
}

export default App;
```



### AND 연산자(&&)를 사용한 조건부 렌더링

조건부 연산자로도 아래와 같이 표현할 수 있다.

```react
import React from 'react';

function App() {
  const name = 'React';
  return (
    <div className="App">{name === 'React' ? (<h1>Hi {name}!</h1>) : null}
      <h2>Hello!</h2>
    </div>
  );
}

export default App;
```



하지만 && 연산자를 사용하여 보다 짧은 코드로 똑같은 작업을 할 수 있다.

```react
import React from 'react';

function App() {
  const name = 'React';
  return (
    <div className="App">{name === 'React' && <h1>Hi {name}!</h1>}
      <h2>Hello!</h2>
    </div>
  );
}

export default App;
```

> 주의 falsy한 값으로 알고 있는 숫자 '0'은 예외적으로 화면에 나타난다.



### undefined를 렌더링하지 않기

리액트 컴포넌트에서는 함수에서 undefined만 반환하여 렌더링하는 상황을 만들면 안 된다.

아래처럼 OR(||) 연산자를 사용하여 오류를 방지할 수 있다.

```react
import React from 'react';

function App() {
  const name = undefined;
  return (
    name || '값이 undefined다.'
  );
}

export default App;
```

cf) div 태그로 감싼 JSX 내부에는 undefine 렌더링은 가능하다.



### 인라인 스타일링

리액트에서 DOM 요소에 스타일을 적용할 때는 문자열 형태로 넣는 것이 아니라 객체 형태로 넣어야 한다.

스타일 이름 중에서 `background-color` 처럼 `-` 문자가 포함되는 이름은 `-` 문자를 없애고 카멜 표기법(camelCase)로 작성해야 한다. (`backgroundColor`)

```react
import React from 'react';

function App() {
  const name = 'React';
  const style = {
    backgroundColor: 'black',
    color: 'aqua',
    fontSize: '48px',
    fontWeight: 'bold',
    padding: 16
  }
  return (
    <div style={style}>{name}</div>
  );
}

export default App;
```



### class 대신 className

JSX에서는 class가 아닌 className으로 설정해줘야 한다.

class로 CSS 클래스를 설정해도 스타일이 적용은 되지만 console 탭에 경고가 나타난다.



### 꼭 닫아야 하는 태그

input 태그의 경우 닫는 태그가 없다.

하지만 JSX에서는 태그를 닫지 않으면 오류가 발생할 수 있다.

```react
<input> </input>
```



태그 사이에 별도의 내용이 들어가지 않는 경우에는 `self-closing` 태그 형태로 작성하면 된다.

```react
<input />
```



### 주석

JSX 내부에서 주석을 작성할 때는 `{/* ... */ }`와 같은 형식으로 작성한다.

만약 일반 JS에서 주석을 작성할 때처럼 아무데나 주석을 작성하면 그대로 화면상에 출력된다.



## ESLint와 Prettier 적용하기

### ESLint

ESLint는 문법 검사 도구이고, Prettier는 코드 스타일 자동 정리 도구다.



## Prettier

JSX를 작성할 때는 코드의 가독성을 위해 들여쓰기를 사용한다.

→ 이러한 스타일을 쉽게 커스터마이징할 수 있다.(Prettier의 장점)



커스터마이징하기 위해서는 src 하위에 `.prettierrc`라는 파일을 생성한 후 아래와 같이 입력하면 된다.(예시)

> .prettierrc

```
{
	"singleQuote": true,
	"semi": true,
	"useTabs": false,
	"tabWidth": 2
}
```

