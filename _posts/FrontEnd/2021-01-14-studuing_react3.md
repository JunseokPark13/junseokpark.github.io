---
title: '[React] React 정리 - 3'
author: Bandito
date: 2021-01-14 12:00:00 +0900
categories: [Study, React]
tags: [Javascript, HTML, FrontEnd, React]
comment: true
description: 'asdsadasd'
---

# React 정리 - 3

공부하면서 생소하거나 잘 모르던 내용들을 정리

+ 이 문서에 있는 내용들
    - [Create 기능](#create-기능)
    - [shouldComponentUpdate](#shouldcomponentupdate)


<br/>

## Create 기능   
*** 

모든 정보 기술은 Create, Read, Update, Delete (CRUD) 에 집합이라고 할 수 있다. 이번에는 React 를 사용하여 정보를 직접 추가하는 Create 관련 기능들을 구현해보려 한다.

![create](https://drive.google.com/uc?export=view&id=1vNxl80UdojotLEXyyCbJ59cmePRhjs_X)

위 사진은 우리가 지금까지 구현했고 앞으로 구현할 내용들을 담은 웹 페이지이다.

+ WEB 을 누르면 하단의 Content 영역이 Welcome, Hello React!! 라는 글을 출력한다.
+ 중앙 목록 중 HTML, CSS, Javascript 를 누르면 각 항목에 대한 제목과 내용으로 하단의 Content 영역이 변경된다.
+ 하단 목록 중 create 를 누르면 Content 영역에 제목과 내용을 입력하고 제출할 수 있는 폼이 출력되고, 이 곳에 값을 입력하면 중앙에 위치한 목록에 추가되게 한다.

<br/>

```javascript
// Control.js
class Control extends Component {
    render() {
      console.log('Control render');
      return (
        <ul>
          <li><a href="/create"
          onClick={function(e){
            e.preventDefault();
            this.props.onChangeMode('create');
          }.bind(this)}
          >create</a></li>
          <li><a href="/update"
          onClick={function(e){
            e.preventDefault();
            this.props.onChangeMode('update');
          }.bind(this)}
          >update</a></li>
          <li><input type="button" value="delete"
          onClick={function(e){
            e.preventDefault();
            this.props.onChangeMode('delete');
          }.bind(this)}
          ></input></li>
        </ul>
      );
    }
  }
```

이후에 구현할 create, update, delete 기능을 포함한 리스트를 만드는 Control 컴포넌트를 제작하였다. 

여기서 delete 만 앵커 태그가 아닌 input 태그로 작성한 이유는 만약 사용자가 이러한 앵커 링크들에 대한 작업을 미리 처리하는 환경을 사용하고 있다면 delete 기능도 앵커 태그로 작성하였을 시 의도치않게 항목들이 삭제되는 일이 일어날 수 있기 때문이다.   


<br/>


```javascript
// App.js
class App extends Component {
  constructor(props){
    super(props);
    this.max_content_id=3;
    ...
    ...
render() {
    var _title, _desc, _article = null; 
    if(this.state.mode === 'welcome'){
      _title = this.state.welcome.title;
      _desc = this.state.welcome.desc;
      _article = <ReadContent title={_title} desc={_desc}></ReadContent>
    } 
    ...
    ...
return(
  ...
  // <Content title={_title} desc={_desc}></Content>
  {_article}
)
```

우선 출력을 위한 Content 와 Create 를 위한 Content 의 구분을 위해 기존에 하나만 존재했던 Content 컴포넌트를 ReadContent 로 변경하고, state.mode 가 welcome 혹은 read 일 때 ReadContent 를 출력하도록 변경하였다.    

또한 현재 state 내의 contents 배열의 수를 저장하기 위한 max_content_id 라는 값을 추가하였다.

return 에 작성되었던 Content 헤더는 _article 로 변경하여 좀 더 유연하게 값을 변경할 수 있도록 한다.  

```javascript
// App.js
...
else if(this.state.mode === 'create'){
      _article = <CreateContent
      onSubmits={function(_title,_desc){
        this.max_content_id +=1;
        var res = this.state.contents.concat({
           id:this.max_content_id,
           title:_title,
           desc:_desc
         });
         this.setState({
          contents:res
         });

        //  this.state.contents.push({
        //    id:this.max_content_id,
        //    title:_title,
        //    desc:_desc
        //  });
        //  this.setState({
        //   contents:this.state.contents
        //  });
      }.bind(this)}
      ></CreateContent>
    }
```

App.js 파일의 render 함수에 작성된 if문에 위 코드와 같은 부분이 추가되었다.   

state.mode 가 create 일 때 _article 을 변경하는 내용이다.    
CreateContent 가 제출된다면 해당 컴포넌트에서 전달받은 _title, _desc 을 contents 배열에 새롭게 추가하는 과정이다.    

여기서 단순히 push 메소드를 사용하여 배열에 값을 추가할 수도 있지만, 이는 배열 자체를 수정해버리는 방식이기 때문에 현명한 방법이라고 할 수 없다.   

각 컴포넌트들은 동작이 일어날 때 마다 렌더링 된다. 컴포넌트 내에서 shouldComponentUpdate() 라는 메소드로 이를 체크하고 제어할 수 있는데, contents.push 를 사용한다면 이전 값과 변경 후의 값을 비교할 때 문제가 생기기 때문에 현명하지 않은 방법이 될 수 있다.   

concat 메소드는 기존의 배열에 새로운 값을 추가한 배열을 반환하는 메소드이다. 이를 사용하여 새로운 배열을 만든 후 state 에 적용한다면 나중에 다른 컴포넌트에서 값의 변경에 더 유연하게 대처할 수 있을 것이다. 


```javascript
// CreateContent.js
class CreateContent extends Component {
    render() {
      console.log('Content render');
      return (
        <article>
          <h2>Create</h2>
          <form action="/create_process" method="post"
            onSubmit={function(e){
              e.preventDefault();
              this.props.onSubmits(e.target.title.value, e.target.desc.value);
            }.bind(this)}
            >
            <p>Title : <input type="text" name="title" placeholder="title"></input></p>
            <p>Text : 
              <textarea name="desc" placeholder="description"></textarea>
            </p>
            <p>
              <input type="submit"></input>
            </p>
          </form>
        </article>
      );
    }
  }
```

새롭게 작성한 CreateContent 컴포넌트는 다음과 같은 구성을 하고있다. 

이 컴포넌트에서는 하나의 form 태그 내에 
1. 제목 작성을 위한 input 태그 (name = "title")
2. 내용 작성을 위한 textarea 태그 (name = "desc")
3. form 제출을 위한 input submit 태그

form 태그에는 위 컴포넌트인 App 에서 전달받은 onSubmits 함수를 onSubmit, 즉 제출 버튼이 눌렸을 때 작동하도록 한다.   
onSubmits 의 인자로는 input 태그에서 입력받은 title 과 desc 를 삽입하면, 제출이 완료되었을 때 App 의 state.contents 에 새로운 배열이 추가되어 렌더링된다. 

## shouldComponentUpdate()
***
```javascript
class TOC extends Component {
    shouldComponentUpdate(newProps, newState){
      console.log('===> TOC render shouldComponentUpdate',
      newProps.data,
      this.props.data )
      if(newProps.data === this.props.data) return false;
      return true;
    }
    ...
```

위에서 언급헀던 shouldComponentUpdate 는 각각의 컴포넌트가 기본적으로 가지고 있는 메소드이다.    
이 메소드는 기본적으로 newProps, newState 두 개의 인자를 받도록 되어있고, 이를 통해 newProps.data === this.props.data 과 같은 비교문으로 기존의 값과 이전의 값이 동일한지를 구분할 수 있다.   

이 메소드의 반환 값이 false 이면 컴포넌트의 render 가 호출되지 않고, true 이면 render 를 호출시킨다.   
이를 이용하여 특정 상황에서는 render 를 호출하지 않게 하여 웹 페이지의 불필요한 render 를 줄이는 것으로 효율성을 향상시킬 수 있다.    



<br/><br/><br/>
_참고한 글이나 영상 :_   
_<https://opentutorials.org/module/4058>_   
