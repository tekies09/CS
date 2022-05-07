다른 팀 개발을 진행 공유를 보다보면 "MVC!디자인패턴이에요" 어느곳은 "MVP 패턴을 1차적으로 빨리 하는거에 목표를 두고있어요!"
라고 말하는데 도대체 어떤걸 의미하는거지?? 다 거기서 거기같은구조인데..라는 느낌을 받아서 한번 정리해보고자 한다..


크게 그림으로 정리해보자!

![](https://github.com/tekies09/CS/blob/main/%EB%94%94%EC%9E%90%EC%9D%B8%ED%8C%A8%ED%84%B4/images/mvc,mvp,mvvm.PNG?raw=true)


그냥 이런 차이가 있구나정도?..

Model 과 view는 그대로고 안에 구성이바뀌구나.. input의 위치가바뀌는구나.. 정도 알고 이제 자세히 뜯어보도록 하자


그리고 들어가기앞서.. Model은 뭐고 !! View는 머에요!!!!!!

Model은 쉽게 말하면 데이터라고보면되고  실상( 데이터 + 상태 + 로직 ) 이렇게 구성되어있다고보면된다.. 
그냥 아 Data처리에 관한 부분이구나~ 하고 생각하자

View는 말그대로 뷰! 
사용자에게 보여지는 UI를 담당한다..  앞에 그림을보면알겟지만 각 디자인에 따라 VIEW가 하는 수행하는 역할이 달라지기도 한다..
그러나! 보여지는 UI를 담당하는건 공통적! 

정리 MODEL => 데이터 다루는거 || VIEW -> UI 임

이제진짜 파헤쳐보자


### MVC 구조


![](https://github.com/tekies09/CS/blob/main/%EB%94%94%EC%9E%90%EC%9D%B8%ED%8C%A8%ED%84%B4/images/mvc.png?raw=true)


짜잔! 숫자가 늘었다.. 그이유는 로직과 함께 설명 

그림을 보면 입력을 Controller가 받는다!그러면 다음과같은 로직으로 진행된다.

1. Controller에서 입력을받아 Model을 업데이트  (Controller는 1개의 Model을 업데이트해줌)

2. 업데이트 된 Model은 그 결과를 반영해서 View를 업데이트 해줘야된다!
	2.1 앗! 어떤 View를 업데이트 해야될까요 ??? => 이 업데이트 할 view를 컨트롤러가 알려준다..

3. Controller가 알려주는 View를 업데이트를 해준다.. (이때 Model 은 N개의 view를 업데이트 할수있따.)
	3.1 엥? model만 view를 업데이트 할수있나요 ?ㅠㅠ
    > view를 업데이트 하는 방법으로는 
    1. view가 polling 하여 자동업데이트
    2. Model에서 view로 Notify 해서 업데이트
    3. view가 Model을 직접 이용해서 업데이트

=> 컨트롤러와 view의 관계는 1 : N !


그래서 다음과같은 그림이 되게된다  

장점 : 그나마 디자인 패턴에서는 가장 단순하다고 볼수있다ㅠㅠ

단점 : 그러면 당연히 Model 과 View 사이에 의존성이.발생 => 그러면 규모가 커지면 ? => 어후.... 네.. 유지보수가어렵습니다..
추가적으로 웹구조는  상관없지만 안드로이드의 구조를 가지게되면 한클래스안에 mvc가 다들어가게되므로..ㅎㅎ;; 필자는 안드로이드 어플개발시 mvi (intent... 여기서는 다루지않음 ㅎㅎ;;) 로 했던것같다.


### MVP 구조

![](https://github.com/tekies09/CS/blob/main/%EB%94%94%EC%9E%90%EC%9D%B8%ED%8C%A8%ED%84%B4/images/mvp.png?raw=true)



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

장점 : MVC 구조의 고질적 문제점이였는 Model과 view 의존성 x

단점 : 그러다보니 view와 presenter의존성이 커짐 + 필요한 클래스가 많아짐.. 


### MVVM 
![](https://github.com/tekies09/CS/blob/main/%EB%94%94%EC%9E%90%EC%9D%B8%ED%8C%A8%ED%84%B4/images/mvvm.png?raw=true)


가운데 중개인기 VIEWMODEL로 바꼇다! 

View에서 입력을 받아 진행된다고하면


1. View로 통해 입력받기
2. View가 Command 패턴으로 viewmodel에 전달
3. viewmodel은 Model에게 요청
4. Model는 viewmodel 요청에 따른 데이터 반환
5. viewmodel은 데이터 가지고만있음 (전달 x)
6. View는 view model과 data binding 하여 화면표시


--> 드디어 중간다리의 의존성이 삭제됫다..

장점 : 의존성 삭제 + 모듈화 개발가능

단점 : mvvm 설계가 넘나어렵긴해요.. ㅠㅠ.. Command 패턴과 DataBinding...

우리가 흔히아는 웹 프론트아키텍처 react,vue..angular는 이걸 쓴다고보면된다..


### 사담

여기서 형상관리 redux 혹은 vuex (형상관리툴)을 얹어서

Flux까지 발전하게되고.. 

Flux는.. 더더더더 어렵다고..한다.. 

Flux가 별로이면.. Observer-Observable Pattern 도가기도하고..

Flux롸 Observable을 섞어쓰기도하고.. 결국 최근에는 MVI쪽으로 되는거같지만..

정리하다보니 프엔 디자인패턴이라는걸 몸소 알게되었따 ㅎㅎ;; 그래도 알아두는게 아키텍처 설계 등 할때 도움이 되었던것같다 ㅎㅎ

MVI는 안드로이드에 더 가깝지만 찾아보니 요즘 다 이방향이라고하고.. 사실 이름도 크게 중요하지않다고한다..

그냥 엄청 빠르게 변하는 메타에 맞춰 카멜레온처럼 변하는게 중요하다고 생각 
