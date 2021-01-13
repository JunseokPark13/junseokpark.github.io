---
title: '[React] React 정리 - 1'
author: Bandito
date: 2021-01-12 12:00:00 +0900
categories: [Study, React]
tags: [Javascript, HTML, FrontEnd, React]
comment: true
description: 'asdsadasd'
---

# React 정리 - 1

공부하면서 생소하거나 잘 모르던 내용들을 정리

+ 이 문서에 있는 내용들
    - [React란?](#react란)
        + [1. JSX 문법](#1-jsx-문법)
        + [2. Component 기반](#2-component-기반)
        + [3.  Virtual DOM](#3-virtual-dom)
    - [React 의 구조](#react-의-구조)
        + [index.html](#indexhtml)
        + [index.js](#indexjs)
        + [App.js](#appjs)
    - [Component 제작](#component-제작)
        + [props](#props)
        + [Component 분리](#component-분리)


<br/>

## React란?
***

React 는 프론트엔드를 위한 라이브러리로, 페이스북이 사용자 UI 구축을 위해 제작하였다. 오직 사용자의 View 에만 초점을 맞추고 있기에 사실상 프레임워크라고 해도 무방할 정도이다. 

React 는 3가지 대표적인 특징을 가지고 있다. 

### 1. JSX 문법 

JSX 는 자바스크립트 안에서 HTML 문법을 사용하여 view를 구성할 수 있게 도와주는 자바스크립트 문법이다. 본래 자바스크립트 내에서 HTML 태그 등의 문법 사용은 불가능하지만, JSX 는 이를 가능하게 해준다. 

### 2. Component 기반 

React 는 컴포넌트 기반 라이브러리로, 여러 부분을 분할하여 코드의 재사용성과 유지보수성을 증가시켜준다. HTML 의 코드 전체 부분을 한 파일에 넣지 않고 각 부분을 따로 파일로 만들어 특정 부분의 수정이 필요한 상황 등에서 용이하다.

### 3. Virtual DOM 

가상 DOM 은 기존의 DOM 한계 탈피를 위한 대안이다. DOM 은 트리구조를 띄고 있어, DOM 의 요소를 많이 수정하면 그 만큼 불필요한 연산이 매번 일어난다.   

가상 DOM 은 변화를 가상 DOM 에서 미리 인지하여 변화시킨다. 이는 실제 DOM이 아니기 때문에 렌더링도 되지 않고, 실제 DOM 보다 변화도 적다. 최종 수정 후 가상 DOM 을 실제 DOM 에게 부여하면 모든 변화를 한번에 렌더링 할 수 있다.   

<br/>

React 는 위와 같은 이유들로 현재 매우 활발히 사용되고 있다. 

<br/>

## React 의 구조 

React 의 작업 환경을 구성하면 public 폴더의 index.html, src 폴더의 App.js, index.js 에 주목할 필요가 있다.

### index.html

public 폴더에 존재하는 **index.html** 은  메인 프로그램인 index.js에 대응하는 파일로, index.js에 의해 읽어와서 렌더링 된 결과가 표시되는 HTML 템플릿이다.   

일반적인 html 파일의 구성을 하고 있지만, body 태그 내부에 존재하는 &lt;div id="root"&gt; 를 볼 수 있다.

### index.js

```javascript
ReactDOM.render(
  <React.StrictMode>
    <App />
  </React.StrictMode>,
  document.getElementById('root')
);
```

src 폴더에 존재하는 **index.js** 파일은 사실상 메인 프로그램으로, 여기에서 HTML 템플릿 및 자바스크립트의 컴포넌트를 조합하여 렌더링하고 실제로 표시한다.

파일에 존재하는 위 코드는 index.html 파일의 root 라는 id 를 가진 태그에 App 이라는 컴포넌트를 적용하겠다는 의미이다.

### App.js 

```javascript
class App extends Component {
  render() {
    return (
      <div className="App">
      </div>
    );
  }
}
```

src 폴더에 존재하는 **App.js** 파일은 컴포넌트를 정의하는 프로그램이다. 실제로 화면에 표시할 내용들을 이 곳에 컴포넌트로 작성하여 정의할 수 있다.   

컴포넌트 작성 시 위와 같은 문법을 지켜야 하며, return 내의 HTML 코드는 반드시 단일 최상위 태그에 감싸져 있어야 한다.



<br/>

## Component 제작 
*** 

React 는 Component 들을 조합하여 웹 페이지를 구성할 수 있다.


```javascript
// App.js
class Subject extends Component {
  render() {
    return (
      <header>
        <h1>WEB</h1>
        World Wide Web
      </header>
    );
  }
}
class App extends Component {
  render() {
    return (
      <div className="App">
        <Subject ></Subject>
      </div>
    );
  }
}
```
```html
<!-- pure.html-->
<header>
    <h1>WEB</h1>
    World Wide Web
</header>
```

위 두 코드는 서로 완벽하게 같은 페이지를 만들어낸다. 위와 같이 React 에서는 삽입하고자 하는 HTML 의 부분을 컴포넌트로 제작하고 이를 App 컴포넌트에 태그 형태로 포함하여 부분적으로 페이지를 구현하는 것이 가능하다.   

<br/>

### props
***
```javascript
class Subject extends Component {
  render() {
    return (
      <header>
        <h1>{this.props.title}</h1>
        {this.props.sub}
      </header>
    );
  }
}

class App extends Component {
  render() {
    return (
      <div className="App">
        <Subject title="web" sub="Yeah"></Subject>
        <TOC></TOC>
        <Content></Content>
      </div>
    );
  }
}
```

또한 JSX 의 props 를 사용하여 컴포넌트로 값을 전달할 수 있다.   
추가한 컴포넌트의 애트리뷰트로 props에서 지정한 id에 대한 값을 작성하면 컴포넌트는 이를 전달받아 코드를 조립한다.    

이러한 방식을 사용하면 코드의 재사용성과 효율을 증가시킬 수 있다. 

<br/>

### Component 분리
***

```javascript
// components/Subject.js
import React, { Component } from 'react';
class Content extends Component {
    render() {
      return (
        <article>
          <h2>HTML</h2>
          HTML is HyperText Markup Language.
        </article>
      );
    }
  }
  export default Content;
```
```javascript
// App.js
import Subject from "./components/Subject";
```

위 코드는 기존에 App.js 파일에 있던 Content 컴포넌트를 별도의 파일로 분리한 것이다.    
별도의 파일에서도 Component 를 import 해서 불러오고 컴포넌트 작성 후 export 하도록 하면 App.js 에서 해당 파일을 불러오는 것으로 적용이 가능하다.

<br/>

## State 
*** 

state 는 props 와 관련이 있다. 컴포넌트를 외부에서 조작할 때는 props, 내부적으로 상태를 관리할 때는 state 를 사용한다. 이는 사용하는 쪽과 구현하는 쪽을 구분하여 편의성을 최대화 하는 과정의 일환이다.   

```javascript
//App.js
class App extends Component {
  constructor(props){
    super(props);
    this.state = {
      subject:{title:'WEB', sub:'World Wide Web'},
       .... 
      ]
    }
  }
  render() {
    return (
      <div className="App">
        <Subject 
        title={this.state.subject.title} 
        sub={this.state.subject.sub}>
        </Subject>
      </div>
    );
  }
}
```

state 를 사용하기 위해서는 state 를 초기화 하는 작업이 먼저 필요하다. constructor 메소드를 사용하면 constructor 가 가장 먼저 시작되어 컴포넌트를 초기화할 수 있다.   

state 의 값으로 사용하고자 하는 값을 작성하여 state 화 시킬 수 있다.   
이렇게 state 로 작성된 값들은 특정 컴포넌트의 애트리뷰트로 삽입할 수 있다.

이는 내부의 값을 숨겨 외부 사람들은 알 수 없게 하는 은닉성의 측면도 지니고 있다.

또한 React 에서는 state 의 값이 변경되면 해당 컴포넌트의 render 메소드도 자동으로 재실행된다. 이렇게 state 값의 변경을 바로 확인할 수 있다.

```javascript
// App.js
class App extends Component {
  constructor(props){
    super(props);
    this.state = {
      contents:[
        {id:1, title:'HTML', desc:'HTML is for information'},
        {id:2, title:'CSS', desc:'CSS is for design'},
        {id:3, title:'Javascript', desc:'Javascript is for interactive'}
      ]
    }
  }
  render() {
    return (
      <div className="App">
        <TOC data={this.state.contents}></TOC>
      </div>
    );
  }
}
```

여러 개의 값을 가진 state 값을 만들고 싶다면 배열 형태로 제작할 수도 있다. 
state 값의 세부 프로퍼티가 아닌 contents 를 직접 넘기는 방식도 사용할 수 있다.

```javascript
// Toc.js
class TOC extends Component {
    render() {
        var lists = [];
        var data = this.props.data;
        var i = 0;
        while(i<data.length){
            lists.push(<li key={data[i].id}>
                <a href={"/content/"+data[i].id}>{data[i].title}</a></li>)
            i+=1;
        }
      return (
        <nav>
          <ul>
            {lists}
          </ul>
        </nav>
      );
    }
  }
```

App 컴포넌트로부터 받은 state 값을 사용하여 HTML 코드를 조립할 수 있다. 이렇게 배열 형태로 제작된 값을 HTML 코드 내에 삽입하여 페이지를 구성하도록 만든다.     

만약 위 처럼 배열을 사용하여 여러 값을 생성할 경우, React 가 각 항목에 대한 유일한 값인 key 를 요구할 수 있다. 이는 직접적으로 드러나는 값은 아니지만, React 가 내부적으로 필요로 하는 값이므로 설정해주는 것이 좋다.   

<!-- <br/>

## 이벤트 적용하기  
***  -->


<br/><br/><br/><br/>
추후 추가 포스팅 예정 


<br/><br/><br/>
_참고한 글이나 영상 :_   
_<https://opentutorials.org/module/4058>_   
