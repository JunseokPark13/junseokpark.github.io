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

<br/>

## Update 기능   
*** 

다음은 CRUD 중 Update 에 대해 구현해보려고 한다. Update 는 Read 와 Create 를 동시에 한다고 생각하면 된다. 선택한 항목에 대한 id, title, desc 을 컴포넌트로 전달하여 input 칸에 기존의 값들이 기본적으로 삽입되어있도록 설정하고, 이를 사용자가 수정할 수 있도록 할 것이다.   

그 전에 구현의 편의성을 위해 약간의 리펙토링 작업을 거치고자 한다.

```javascript
// App.js
getReadContent(){
    for(var i = 0; i<this.state.contents.length; i++){
      var data = this.state.contents[i];
      if(data.id === this.state.selected_content_id){
        return data;
      }
    }
  }
```

현재 id 와 같은 state.contents 의 값을 가져오는 반복문을 별도의 함수로 분리한 모습이다. 이를 객체에 저장하는 것으로 쉽게 값을 가져올 수 있게 되었다. 

```javascript
// App.js
 else if(this.state.mode === 'update'){
      var _content = this.getReadContent();
      _article = <UpdateContent
      data={_content}
      onUpdates={function ...
```

content 영역의 Update 기능을 위해 UpdateContent 라는 컴포넌트를 새롭게 만들었다. 이 컴포넌트에 현재 ReadContent 를 통해 선택하고 있는 state.contents 의 값을 속성으로 전달한다.

```javascript
// UpdateContent.js
class UpdateContent extends Component {
  constructor(props){
    super(props);
    this.state = {
      id:this.props.data.id,
      title:this.props.data.title,
      desc:this.props.data.desc
    }
    this.inputFormHandler = this.inputFormHandler.bind(this);
  }
```

이전에도 언급했듯이 props 로 받아온 값들은 read-only, 즉 읽기 전용이므로 변경이 불가능하다. 이 값들을 input 태그의 value 로 삽입하여 기존의 값을 출력시키는 것은 가능하지만, 사용자가 새로운 값을 입력하고 submit 하더라도 수정은 할 수 없다는 뜻이다.    

하지만 state 는 수정이 가능한 값들이다. 이를 처리하기 위해 UpdateContent 컴포넌트의 state 에 속성으로 받아온 data의 id, title, desc 값을 넣어준다.   

```javascript
// UpdateContent.js 의 render()
<form action="/create_process" method="post"
            onSubmit={function(e){
              e.preventDefault();
              //this.props.onUpdates(e.target.id.value, e.target.title.value, e.target.desc.value);
              this.props.onUpdates(
                this.state.id,
                this.state.title,
                this.state.desc
              )
            }.bind(this)}
          >
          ...
```

form 태그에서는 submit 버튼이 눌렸을 때 상위 App 컴포넌트의 onUpdates 메소드에 form 태그 내의 input 태그들에서 입력된 값들을 전달하는 코드를 작성한다.

```javascript
// UpdateContent.js
inputFormHandler(e){
    this.setState({[e.target.name]:e.target.value})
  }
```
```javascript
// UpdateContent.js 내의 render() 
<input type="hidden" name="id" value={this.state.id}></input>
            <p>Title : <input type="text" name="title" 
            value={this.state.title} 
            onChange={this.inputFormHandler}
            placeholder="title!"></input></p>
<p>Text : 
  <textarea name="desc" 
      value={this.state.desc}
      onChange={this.inputFormHandler}
      placeholder="description!"></textarea>
</p>
<p> <input type="submit"></input> </p>
```

inputFormHandler 함수는 UpdateContent 컴포넌트에 선언한 것이다. 이 함수는 인자로 받은 항목의 값을 state 에 반영하는 역할을 수행한다. 

```javascript
// App.js
else if(this.state.mode === 'update'){
      var _content = this.getReadContent();
      _article = <UpdateContent
      data={_content}
      onUpdates={function(_id,_title,_desc){
        var clone = Array.from(this.state.contents);
        for(var i=0; i<clone.length; i++){
          if(clone[i].id === _id){
            clone[i] = {id:_id, title:_title, desc:_desc};
            break;
          }
        }
         this.setState({
          contents:clone,
          mode:'read'
         });
      }.bind(this)}
      ></UpdateContent>
```

UpdateContent 컴포넌트에서 받아온 값들을 App 컴포넌트의 if 문에서 처리하는 과정이다.   

이전에 언급했던 것 처럼 직접 state.contents 를 수정하는 것은 효율적이지 않을 수 있다. 때문에 contents 자체를 복사한 clone 객체를 수정한 뒤 이를 setState 로 contents에 적용하는 방법을 수행한다.   

그리고 update 를 수행한 뒤에는 수정한 내용을 볼 수 있도록 mode 를 'read' 로 변경하면 수정과 동시에 수정된 내용을 ReadContent 가 불러올 수 있게 된다.





<br/><br/><br/><br/>
추후 추가 포스팅 예정 


<br/><br/><br/>
_참고한 글이나 영상 :_   
_<https://opentutorials.org/module/4058>_   
