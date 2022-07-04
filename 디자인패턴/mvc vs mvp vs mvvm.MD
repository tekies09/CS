다른 팀 개발 진행 공유를 염탐 하다보면 우린 MVC ~ 어디에는 MVP , 그리고 MVVM 까지.. 정말 다양한 패턴들이 많다.. 그때마다 눈가리고 아웅을 해왔지만 이번기회를 통해 자세히 알아보고 그들의 정보를 빠르게 습득해보도록 하자!

크게 그림으로 보자면 다음과같다.

![](https://github.com/tekies09/CS/blob/main/%EB%94%94%EC%9E%90%EC%9D%B8%ED%8C%A8%ED%84%B4/images/mvc,mvp,mvvm.PNG?raw=true)

#### 겁먹지마세요!! 그냥 이런차이가 있다 정도 느낌이면 충분해요~ 

Model 과 view는 그대로고 안에 구성이바뀌구나.. input의 위치가바뀌는구나.. 정도 알고 이제 자세히 뜯어보도록 하자


#### 잠깐! 그전에 앞서서 기존 지식부터 습득하고 넘어가자

- Model은 뭐고 !! View는 머에요!!!!!!
> 알고 있다면 바로 구조 파악으로 넘어가도 좋다

> Model 같은 경우에는 쉽게 말하면 데이터 자체라고 보면되고 (데이터 + 상태 + 로직) 으로 구성이 되어있다. 감이 안온다면 그냥 쉽게 Data에 처리에 관한 부분이구나 하고 넘어가도록 하자.

> View 와 같은경우도 말그대로 사용자에게 보여주는 UI를 의미하고 그림을 보면 알겠지만 각 디자인에 따라 VIEW의 역할이 달라지기도 하지만 보여지는 UI를 담당하는것은 공통적이다. 

- 한줄요약 
  - MODEL : 데이터  ||  VIEW  :  UI 
  

### MVC 구조


![](https://github.com/tekies09/CS/blob/main/%EB%94%94%EC%9E%90%EC%9D%B8%ED%8C%A8%ED%84%B4/images/mvc.png?raw=true)


짜잔! 숫자가 늘었다.. 메인 로직을 확인하면서 한번 유의 깊게 보도록 하자.

#### 메인 로직

그림을 보면 입력을 Controller가 받는다!그러면 다음과같은 로직으로 진행된다.

1. Controller에서 입력을받아 Model을 업데이트  (Controller는 1개의 Model을 업데이트해줌)

2. 업데이트 된 Model은 그 결과를 반영해서 View를 업데이트 해줘야된다!
	2.1 앗! 어떤 View를 업데이트 해야될까요 ??? => 이 업데이트 할 view를 컨트롤러가 알려준다..

3. Controller가 알려주는 View를 업데이트를 해준다.. (이때 Model 은 N개의 view를 업데이트 할수있다.)
	3.1 엥? model만 view를 업데이트 할수있나요 ?ㅠㅠ
    > view를 업데이트 하는 방법으로는 
    > 1. view가 polling 하여 자동업데이트
    > 2. Model에서 view로 Notify 해서 업데이트
    > 3. view가 Model을 직접 이용해서 업데이트

=> 컨트롤러와 view의 관계는 1 : N !


#### 장단점 

- 장점 : 우리가 현재 포스팅에서 공부할 패턴중에서는 가장 단순하다고 볼수있다

- 단점 : Model 과 View 사이에 의존성이 발생하게된다 => 그러면 규모가 커지면 ? => 어후.... 네.. 유지보수가어렵습니다.. 추가적으로 웹구조는  상관없지만 안드로이드의 구조를 가지게되면 한클래스안에 mvc가 다들어가게되므로.. 결과는 안봐도 뻔하게된다.. ㅎㅎ;; 필자는 안드로이드 어플개발시 mvi (intent... 여기서는 다루지않음 ㅎㅎ;;) 로 했던것같다.



### MVP 구조

![](https://github.com/tekies09/CS/blob/main/%EB%94%94%EC%9E%90%EC%9D%B8%ED%8C%A8%ED%84%B4/images/mvp.png?raw=true)

#### 메인 로직

Controller가 Presenter로.. input을 이제 view에서 받는다!!! 

Presenter의 역할은 view에서 입력받아 model 가공해서 다시 view로 전달해준다!! 

간단하게말하면 view model간의 통신을 Presenter가 오작교 마냥 다리 역할을 나줘서 해준다

그림을 보면 입력이 view로 받아서 진행된다고하면

1. View로 통해 입력받기
2. View가 Presenter로 입력에 따른 데이터 요청  (view는 1개의 presetner만...)
3. Presenter는 Model에게 요청
4. Model는 Presenter 요청에 따른 데이터 반환
5. Presneter은 받은 데이터를 view게 전달 (presenter는 1개의 view에게만..)
6. View는 데이터에따라 Update해줌 

=> view와 presenter => 1: 1 구조!

#### 장단점 

- 장점 : MVC 구조의 고질적 문제점인 Model과 view 의존성 x 을 개선한 아키텍처

- 단점 : view와 presenter의존성이 커짐 => 그에 따른 필요한 클래스가 많아짐.. 



### MVVM 

![](https://github.com/tekies09/CS/blob/main/%EB%94%94%EC%9E%90%EC%9D%B8%ED%8C%A8%ED%84%B4/images/mvvm.png?raw=true)

#### 메인로직 

MVP에 구조에서 가운데 중개인 역할을 하는것이 VIEWMODEL로 바꼇다! 

View에서 입력을 받아 진행된다고하면


1. View로 통해 입력받기
2. View가 Command 패턴으로 viewmodel에 전달
3. viewmodel은 Model에게 요청
4. Model는 viewmodel 요청에 따른 데이터 반환
5. viewmodel은 데이터 가지고만있음 (전달 x)
6. View는 view model과 data binding 하여 화면표시


--> 드디어 중간다리의 의존성이 삭제됫다..

#### 장단점

- 장점 : 의존성 삭제 + 모듈화 개발가능

- 단점 : mvvm 설계가 어려운것이 단점이라고 한다. 추가적으로 Command 패턴과 DataBinding...

우리가 흔히아는 웹 프론트아키텍처 react,vue..angular는 이걸 쓴다고보면된다..


### 추가적으로...

이러한 구조에 형상관리까지 얹혀져서 요새는 사용되는걸로 알고있고 그러다 보니 점차 발전해서 Flux까지.. 그러면 당연히? 그만큼 더어렵다고 한다..

이러한 것에도 만족하지 못하면 Oberserver-Observable Pattern 도 가게되고  이렇게 하나만 추구하지않고 Flux + Observable을 섞어쓰기도 하고 아마 프로젝트 분석을 해서 오래 지속가능한 아키텍처를 설계하는것이 핵심인것같다.

최근에는 MVI?? 도있다고하고.. 후.. 넘나어려운것 ㅠㅠ... 요약을 하자면 다음과 같다.

> 한줄요약 : 패턴간의 우위를 따지기 보다는 본인의 프로젝트 분석을 잘해서 알맞는 아키텍처를 설계하고 오래 지속가능하도록 노력하는게 가장 BEST!  
