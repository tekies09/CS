디자인 패턴의 길은 멀고도 끝이없는법

하지만 차근차근 하나씩 정리해서 알아보자

## MVC1 

![image mvc1](https://github.com/tekies09/CS/blob/main/%EB%94%94%EC%9E%90%EC%9D%B8%ED%8C%A8%ED%84%B4/images/mvc1.png?raw=true)

JSP로 VIEW + CONTROLLER를 한방에 다뤄주고

JAVA BEAN에서 DB를 읽어오고 처리를해준다.

단순하고 구현난이도가 쉽다!! 라는게 특징이지만..

JSP 하나에서 모든걸 다 처리하다보면 당연히 엄청.. 읽기도힘들고 까다로워진다..

=> 그말은 즉 재사용성도 떨어지고 유지보수가 떨어진다는뜻


## MVC2

![image mvc2](https://github.com/tekies09/CS/blob/main/%EB%94%94%EC%9E%90%EC%9D%B8%ED%8C%A8%ED%84%B4/images/mvc2.png?raw=true)

MVC1 보다 이미지만 봐도 복잡하게 생기긴 하였다.

### 로직
1. User가 Controller (Servlet) 를 통해 입력
2. Controller 가 처리할 클래스를 선택해 모델로 넘겨줌
3. DB에 대한 접근이 아니라 View 관한 부분이면 View로 접근
4. Model 에서 쿼리를 통해 DB에접근하여 저장후 저장된 결과를 view로 보낸다.
5. View단에서 User로 리턴


MVC1과 비교하자면 많은 부분이 개선됨을 알수있다. 왜냐하면 MVC1 방식을 보완하기위해 나온거니까..
JSP (View) 단에서는 보여지는 뷰만 담당하는걸 알수있고 모듈화가 된만큼 그만큼 유지보수가 높아짐을 알수있지만.. MVC1에 비해 조금더 복잡해짐을 알수있따.



## Spring MVC

![srping mvc](https://github.com/tekies09/CS/blob/main/%EB%94%94%EC%9E%90%EC%9D%B8%ED%8C%A8%ED%84%B4/images/springmvc.PNG?raw=true)

더더더더ㅓ 복잡해졋다. 

### 로직 
1. 유저의 입력을 처리하는 FrontController(DispatcherServlet)을 통해 입력을받음
2. FrontController(DispatcherServlet는 HandlerMapping을 이용해 어떤 컨트롤러가 호출됬는지 return 받는다.
3. FrontController(DispatcherServlet는 return 받은 컨트롤러를 Hadnler Adapter를 이용해 접근하기
4. HandlerAdapter로 호출된 Controller는 Service를 호출하고 Service에서 비즈니스 로직을 처리한후 Model에 저장해준다.
5. HandlerAdapter로 호출된 Controller는 viewname으로 제작하여 HadnlerAdapter를거쳐 FrontController(DispatcherServlet) 에게 전달해줌
6. FrontController(DispatcherServlet)는 받은 view name을 이용해  ViewResolver에 처리결과를 생성할 뷰를 결정해 달라고 요청후 View를 받는다.
7. FrontController(DispatcherServlet)는 받은 View를 이용해 View단으로 넘겨준다.
8. View는 응답을 하기전 Model로부터 렌더링 받은후에 응답한다.

SpringMVC 는 MVC2와 어느정도 흐름이 비슷하다.






