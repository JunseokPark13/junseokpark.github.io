---
title: '[Python] 네이버 카페에 덧글 달아주는 매크로 제작기 - 2'
author: Bandito
date: 2020-12-18 20:40:00 +0900
categories: [Study, Python]
tags: [Python, toy]
toc: false
comment: true
---

## - 내가 만들고자 하는 것
***
지정된 페이지에서 지속적으로 새로고침을 하면서 조건에 맞는 글이 올라오면   
해당 글에 들어가 빠르게 댓글을 달 수 있는 프로그램을 만들어보자



## - 제작 과정
***

저번에는 로그인을 하고 지정된 링크의 카페에 진입하는 것 까지 해보았다.   
오늘은 '일단' 테스트용 카페에서 잘 구동되도록 기본적인 기능들을 완성해보고자 한다.   


### - 네이버 카페의 프레임 구분

우선 네이버 카페의 html 구조에 대해 알아야한다.   

![Alt text](/assets/img/posting/f12_2.PNG)
<br/>

우선 우리는 게시물의 제목을 이용하여 조건을 따진다고 해보자.   
그렇다면 이전처럼 개발자 모드에서 원하는 요소를 클릭해서 해당 요소의 정보를 확인하면 될 것이다.

하지만 네이버 카페는 게시글의 목록들이 있는 프레임과 바깥 프레임을 구분하고 있다.

![Alt text](/assets/img/posting/f12_3.PNG)
<br/>

위 사진과 같 게시글 목록은 content-area 라는 div에서 cafe_main 이라는 iframe 안에 들어있는 것을 확인할 수 있다.    

간단하게 말하면, 게시글 목록을 접근할 때와 다른 부분(카테고리, 로그인 버튼 등)을 접근할 때는 프레임을 변경해주면 된다는 것이다.   


### - 원하는 게시판 접근

```python
driver.find_element_by_xpath('//*[@id="menuLink1"]').click()
time.sleep(1)
```

우선 카페 메인에서 바로 탐색하는 것이 아닌, 특정 게시판을 들어가고자 한다.   
내가 들어가고 싶은 게시판은 '자유게시판'이므로 xpath를 확인하여 접속하도록 코드를 작성한다.   

### - 게시글 제목 확인

다음은 게시물의 제목들을 확인하여 조건에 맞는 게시물이 있는지 확인할 차례다.
아까 게시물 제목의 요소를 확인했던 것이 기억나는가? 게시물의 클래스명은 'article' 이었다.   
이를 활용할려 했으나, 문제는 공지 글도 클래스명이 article 이라는 점이다.   
나는 일반 게시물만 활용하고 싶으므로 다른 속성들을 확인해보았다.   

![Alt text](/assets/img/posting/terminal_onclick.PNG)
<br/>

위와 같이 공지는 onclick 속성 중 gnr.notice 을 갖고있고, 일반 게시물은 gnr.title을 갖고있다.   
이를 활용해서 일반 게시물들을 가려내기로 했다.

```python
driver.switch_to.frame('cafe_main') # 프레임을 게시판 프레임으로 변경
pageString = driver.page_source     # 현재 페이지 소스를 획득
bsObj = BeautifulSoup(pageString, 'html.parser') # bsObj에 페이지 내용을 저장
title = bsObj.find_all(class_="article")
# 저장된 내용 중에서 class 가 article 인 요소 추출

article = "gnr.title"

for i in title:
  if article in i['onclick']:
    print(i.getText().strip())
  # 요소들 중에서 제목으로 쓰이는 텍스트들 출력
```

프레임을 변경 후 BeautifulSoup을 사용해서 페이지 정보를 긁어오는 과정이다.   
우리가 필요한 것은 게시글 제목 뿐이므로 원하는 클래스를 가진 요소들만 getText()를 사용해 반복문으로 출력한다.   
왠지는 모르겠는데, 단순히 게시글 제목만 가져오면 텍스트 앞뒤로 엄청난 양의 공백들이 딸려나온다.   
이를 지우고 깔끔하게 확인하기 위해 strip()도 사용해줬다.

![Alt text](/assets/img/posting/terminal_1.PNG)
<br/>

위 사진처럼 게시물들의 제목이 잘 추출된 것을 볼 수 있으면 성공


### - 조건에 맞는 게시물 들어가기

조건에 맞는 게시물을 찾는 것은 if문을 사용하면 되니까 어렵지 않다.  
원하는 게시물을 들어가려면 그 게시물을 찾기 위한 적절한 경로를 알아야 한다.   

```python
//*[@id="upperArticleList"]/table/tbody/tr/td[1]/div[2]/div/a    #공지
//*[@id="main-area"]/div[4]/table/tbody/tr[1]/td[1]/div[3]/div/a # 게시글1
//*[@id="main-area"]/div[4]/table/tbody/tr[2]/td[1]/div[3]/div/a # 게시글2
//*[@id="main-area"]/div[4]/table/tbody/tr[3]/td[1]/div[3]/div/a # 게시글3
```

맨 위 글은 공지이고 그 다음부터는 가장 최근에 작성된 순서로 정렬된 게시글들이다.   
공지를 찾는 것은 아니니 제외하고, 그 아래의 게시글들은 중간의 tablerow, 즉 tr 값만 변하는 것을 알 수 있다.    
간단하게 tr 값만 변경하여 경로를 조립하면 될 것 같아 다음과 같이 코드를 작성하였다.

```python
block1 = '//*[@id="main-area"]/div[4]/table/tbody/tr['
block2 = ']/td[1]/div[3]/div/a'
# xpath 를 조립하기 위한 경로의 앞, 뒷부분

article = "gnr.title"
keyword = "test" # 찾고자 하는 제목 키워드
count = 1        # 게시글 카운트

for i in title:
    if article in i['onclick']:
        print(i.getText().strip())
        if keyword in i.getText().strip():
            xpath = block1 + str(count) + block2
            driver.find_element_by_xpath(xpath).click()
            break
        # 키워드가 포함된 글을 발견하면 해당 게시물에 접속 후 반복문 탈출
        count+=1 # 1씩 증가시키며 다음 게시물 탐색
```

count 를 1으로 해준 이유는 일반 게시물의 tr 값은 1부터 시작하기 때문이다.   
이렇게 하면 지정된 키워드 조건에 맞는 게시물에 들어가는 것 까지 가능해졌다.


### - 페이지 새로고침

우리가 고려해야 할 점 중 가장 중요한 것은, 게시물이 언제 올라올지 모른다는 것이다.   
그래서 임의로 게시판을 새로고침하여 지속적으로 체크가 가능하도록 만들 것이다.

네이버 카페에서는 대문을 통해 들어간 게시판에서 새고로침을 누르면 다시 메인 대문으로 보내진다.   
일반적인 새로고침은 사용할 수 없으므로 다른 방법을 사용하였다.

```python
success = True # while 문의 작동을 구분할 bool 변수

while success:
    pageString = driver.page_source
    bsObj = BeautifulSoup(pageString, 'html.parser')
    title = bsObj.find_all(class_="article")
    time.sleep(0.5)
    #페이지가 새로고침될 때 마다 페이지 정보를 받아와 title에 저장
    for i in title:
        if article in i['onclick']:
            print(i.getText().strip())
            if keyword in i.getText().strip():
                xpath = block1 + str(count) + block2
                driver.find_element_by_xpath(xpath).click()
                success=False
                break
                #조건에 맞는 게시물을 찾으면 접속하고 success를 false로 변경
            count+=1
    count=1
    if success:
        driver.switch_to.parent_frame()
        driver.find_element_by_xpath('//*[@id="menuLink1"]').click()
        driver.switch_to.frame('cafe_main')
        # 찾지 못했을 경우 새로고침 대신 다시 게시판에 들어오는 과정을 거침
```

게시물 탐색 및 접속에 성공여부를 판단하는 success 변수를 추가하였다. 성공하지 못했다면 계속 게시판에 접속하며 조건에 맞는 게시물이 있는지 확인한다.   
이를 위해서는 새롭게 페이지에 접속할 때 마다 정보를 가져와 저장해야 한다.   

또한 새로고침을 하기 위해 눌러야 하는 게시판 카테고리는 게시판과 다른 프레임에 존재하므로, 일시적으로 프레임을 부모 프레임으로 변경했다가 게시판 접속이 끝나면 다시 게시판 프레임으로 변경하는 과정을 거친다.   

이를 통해서 지속적으로 게시판에 올라오는 게시물을 체크할 수 있게 되었다.
하지만 이렇게 지속적으로 같은 행위를 빠르게 반복한다면 문제가 발생할 수 있으니 조심해야 하는데.. 이 부분은 사용 시간을 조절하는 방식 외에는 해결 방법을 잘 모르겠다.

### - 덧글 달기

이는 우리가 로그인을 할 때 구현했던 코드들을 생각하면 간단하게 구현 가능하다.   

```python
time.sleep(0.5)
driver.find_element_by_xpath('//*[@id="app"]/div/div/div[2]/div[2]/div[4]/div[2]/div[1]/textarea').send_keys("1")
driver.find_element_by_xpath('//*[@id="app"]/div/div/div[2]/div[2]/div[4]/div[2]/div[2]/div[2]/a').click()
```

단순히 댓글 작성란의 xpath 에 아무런 값이나 보내고 댓글 작성 버튼에 클릭 신호를 보내는 것으로 처리했다.   
이 코드에 단점이 있다면.. 네이버 카페에서는 댓글이 100개가 넘어가면 댓글 페이지가 넘어가게 되는데, 만약 내가 달려는 댓글이 100번째 이후라면 매크로가 제대로 요소를 찾지 못할 수도 있다는 것.   
댓글 페이지가 다르면 댓글 등록 버튼의 xpath 중 4번째 div 값이 변경되어버린다.   

하지만 게시글이 등록된 직후 바로 댓글을 작성하는 것이고... 큰 문제는 되지 않을 것 같다.


### - 완성!

제대로 동작하는 것을 확인했다! 매크로는 접속 후 지속적으로 게시판을 새로고침하다가 조건에 맞는 게시글이 올라오면 해당 글에 덧글을 작성했다.   

실제 카페에서도 사용해보고 싶은 마음이 굴뚝같지만... 싼 값에 고기 먹기 참 힘든 것 같다.   


아무튼 기본적인 기능은 완성했지만, 아직 부족한 부분이 많아보인다.   
나중에 시간이 된다면 부족했던 부분을 조금씩 보완해보고싶다..
