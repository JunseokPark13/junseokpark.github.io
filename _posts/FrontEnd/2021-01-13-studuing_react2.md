---
title: '[React] React 정리 - 2'
author: Bandito
date: 2021-01-13 12:00:00 +0900
categories: [Study, React]
tags: [Javascript, HTML, FrontEnd, React]
comment: true
description: 'asdsadasd'
---

# React 정리 - 2

공부하면서 생소하거나 잘 모르던 내용들을 정리

+ 이 문서에 있는 내용들
    - [이벤트 적용하기](#이벤트-적용하기)


<br/>

## 이벤트 적용하기  
*** 

이벤트와 관련된 작업을 추가하기 위해서는 이전에 자바스크립트 공부에서 언급했던 bind 와 state 의 성질에 대해 이해해야한다.

우선 이벤트를 구현하기 위한 state 값들의 준비와 render 내의 코드들을 작성하였다. 


```javascript
this.state = {
      mode:'welcome',
      selected_content_id:2,
      welcome:{title:'welcome', desc:'Hello React!!'},
      contents:[
        {id:1, title:'HTML', desc:'HTML is for information'},
        {id:2, title:'CSS', desc:'CSS is for design'},
        {id:3, title:'Javascript', desc:'Javascript is for interactive'}
      ]
}
render() {
    var _title, _desc = null;
    if(this.state.mode === 'welcome'){
      _title = this.state.welcome.title;
      _desc = this.state.welcome.desc;
    } 
    else if(this.state.mode === 'read'){
      for(var i = 0; i<this.state.contents.length; i++){
        var data = this.state.contents[i];
        if(data.id === this.state.selected_content_id){
          _title = data.title;
          _desc = data.desc;
          break;
        }
      }
    }
    return ( 
      ...
    <Content title={_title} desc={_desc}></Content>
    
```

기본으로 state 의 mode 는 'welcome' 이라는 값을 가지고 있고, mode 가 'read' 로 변경되었을 때 contents 의 id 에 따라 Content 태그의 속성들이 변경되는 구조를 취한다. 

<br/>

```javascript
// App.js
<Subject 
        title={this.state.subject.title} 
        sub={this.state.subject.sub}
        // this.state.mode = 'welcome'
        onChangePage={function(){
          this.setState({mode:'welcome'});
        }.bind(this)}
        >
</Subject>
```
```javascript
// Subject.js
class Subject extends Component {
    render() {
      console.log('Subject render');
      return (
        <header>
          <h2><a href="" onClick={function(e){
            e.preventDefault();
            this.props.onChangePage();
          }.bind(this)}>{this.props.title}</a></h2>
          {this.props.sub}
        </header>
      );
    }
  }
```

첫번째로 Subject 의 h2 태그를 누르면 state 의 mode 가 'welcome' 으로 변경되도록 하는 코드이다.    

App.js 에서 넘겨줄 속성으로 onChangePage 라는 메소드를 선언하였다.    

여기서 중요한 것은 메소드를 정의하는 중괄호에 .bind(this) 를 부착해주어야 한다는 것인데, 그 이유는 함수의 this 가 지정되지 않은 상태이기 때문이다.   

기본적으로 render 함수 내에서 this 는 자신이 속한 컴포넌트(App)를 가리키지만, 새로 선언하는 함수 내에서는 그렇지 않다.    
그렇기 때문에 bind(this) 를 사용한다면 this 가 App 으로 설정되어 제대로 state 인식이 가능하게 된다.

또한 이벤트 내에서 state 값을 변경하기 위해서는 직접 값을 변경하는 것이 아닌 this.state 메소드를 사용하여야 한다.   

<br/>

다음으로 살펴볼 것은 Subject.js 의 코드이다.    

React 내의 html 코드는 기존의 것과 조금 달라서 이벤트를 부착하기 위해서는 onclick 이 아닌 **onClick** 에 값을 부여해야 한다.    

또한 앵커 태그에 부착된 이벤트를 작동시키면 자동으로 페이지가 새로고침 되기 때문에 이벤트의 매개변수인 e 를 사용하여 e.preventDefault() 메소드로 클릭 시의 기본 동작을 정지시켜야 한다.   

나머지는 props 로 전달된 함수인 onChangePage() 를 호출하면 제대로 작동하게 된다. 

<br/>

```javascript
// App.js
<TOC 
    data={this.state.contents}
    onChangePage={function(id){
      this.setState({
        mode:'read',
        selected_content_id:Number(id)
      })
    }.bind(this)}></TOC>
```
```javascript
// Toc.js
render() {
    var lists = [];
    var data = this.props.data;
      for(var i=0; i<data.length; i++){
        lists.push(<li key={data[i].id}>
            <a href={"/content/"+data[i].id} 
              data-id = {data[i].id}
              //onClick={function(id,e)}
              onClick={function(e){
                e.preventDefault();
                this.props.onChangePage(e.target.dataset.id);
                //this.props.onChangePage(id);
              }.bind(this)}
              // bind(this, data[i].id)
            >{data[i].title}</a></li>)
        }
```

다음은 페이지 중간의 리스트를 생성하는 Toc 부분이다.   

리스트 항목을 선택하면 state 의 mode 가 read 로 변경되면서 하단의 Content 태그의 값들이 변경된다. 이를 위해서는 누르는 링크에 해당하는 contents 의 id 값을 전달할 필요가 있다.   

Toc.js 에서 선언된 함수의 function 인자인 e 는 이벤트가 발생한 태그를 가리킨다.    
onChangePage 의 인자로 값을 전달하기 위해서 함수가 선언된 &lt;a&gt; 내에 속성으로 전달하고자 하는 값을 입력해둔다면 e 객체를 통해 값을 지정할 수 있다.   

태그의 속성명을 data-XX 로 지정한다면 e 객체의 dataset을 통해 접근이 가능하다.   
위 코드는 data-id = data[i].id 로 저장을 하고있기 때문에 e.target.dataset.id 를 onChangePage의 인자로 넘겨주면, App.js 에 있는 TOC 태그에서 선언한 onChangePage 의 매개변수로 넘어가 참조가 가능하다.   

여기서 주의해야 할 점은, 이 값이 정수라 할지라도 다른 자료형으로 넘어갈 수 있기 때문에 정수형 값을 사용하기 위해서는 Number(인자) 메소드를 이용하여야 한다.









<br/><br/><br/><br/>
추후 추가 포스팅 예정 


<br/><br/><br/>
_참고한 글이나 영상 :_   
_<https://opentutorials.org/module/4058>_   
