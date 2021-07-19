---
title: '[React] React 정리 - 4'
author: Bandito
date: 2021-01-15 12:00:00 +0900
categories: [Study, React]
tags: [Javascript, HTML, FrontEnd, React]
comment: true
description: 'asdsadasd'
---

# React 정리 - 4

공부하면서 생소하거나 잘 모르던 내용들을 정리

+ 이 문서에 있는 내용들
    - [Update 기능](#update-기능)
    - [Delete 기능](#delete-기능)


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




<br/>

## Delete 기능   
*** 

Delete 기능은 가장 간단하게 구현할 수 있다. 

```javascript
// App.js
<Control
    onChangeMode={function(_mode){
      if(_mode === 'delete'){
          var clone = Array.from(this.state.contents);
          if(window.confirm('Really?')){
            for(var i=0; i<clone.length; i++){
              if(clone[i].id === this.state.selected_content_id){
                  clone.splice(i,1);
                  break;
                }
              }
            this.setState({
              contents:clone,
              mode:'welcome'
            })
          }
        }
      else{
        this.setState({
          mode:_mode
       })
      }}.bind(this)}></Control>
```

이전에 구현하였던 Control 컴포넌트는 기본적으로 mode 를 변경하는 기능만을 수행했다.   

여기에 전달받은 _mode 가 delete 일 때 confirm 메소드를 통해 삭제 여부를 확인, 취소로 전달받은 후 확정되었다면 현재 선택된 id에 해당하는 contents 배열 항목을 삭제하고 setState 로 이를 적용하는 과정으로 마무리지을 수 있다.


<br/><br/><br/>


나중에 [React Router Dom](https://youtu.be/WLdbsl9UwDc) 이라는 강의도 들어보고자 한다



<br/><br/><br/>
_참고한 글이나 영상 :_   
_<https://opentutorials.org/module/4058>_   
