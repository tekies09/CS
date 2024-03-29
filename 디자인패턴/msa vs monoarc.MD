모노리틱 아키텍처 와 MSA 아키텍처에 대해 알아보자

## 모노리틱 아키텍처

모노리틱 아키텍처 => 기존 사용하던 개발방법 

즉 하나의 Application 안에 모든 기능을 다 넣은 구조이다.

그림으로보면 다음과같다.

![모노아키텍처1](https://github.com/tekies09/CS/blob/main/%EB%94%94%EC%9E%90%EC%9D%B8%ED%8C%A8%ED%84%B4/images/monoarc.PNG?raw=true)

여기서 우리가쓰는 SpringBoot 3 Layer로 확장해서본다면..

> SpringBoot 3 Layer에 관한 부분은 여기를 참조하길 바란다 [스프링부트의 주요 3 계층](https://github.com/tekies09/CS/blob/main/SpringBoot/spring3layer.MD)


![모노아키텍처2](https://github.com/tekies09/CS/blob/main/%EB%94%94%EC%9E%90%EC%9D%B8%ED%8C%A8%ED%84%B4/images/monoarc2.PNG?raw=true)

### 장단점

#### 장점 
- 배포 테스트 편리
- 트랜젝션 관리 편리

#### 단점 
- 규모가 확장되면 전체로 확장해야됨
- 대규모 프로젝트에 도입을 한다면 전체적인 시스템 구조에 이해가 어려워짐
- 하나가 고장나면 전체 영향
- 만약 데이터 특성을 여러개 쓴다면.. 필자의 경우 대피소 재난서비스를 하는데 뉴스기사 크롤링은 NO-SQL // 대피소정보는 RDBMS가 나앗지만.. 혼용하기 어려워서 NOSQL로 통일함.


## MSA (마이크로 서비스 아키텍처)

MSA => 컴포넌트 별로 작은 서비스로 구성하기

그림으로보면 다음과같다.

![msa아키텍처](https://github.com/tekies09/CS/blob/main/%EB%94%94%EC%9E%90%EC%9D%B8%ED%8C%A8%ED%84%B4/images/msaarc.PNG?raw=true)

추가적으로 고려해야할 부분

> 데이터분리 : 서비스별 별도의 DB를사용함 => 트렌젝션을 묶어서 처리할수없음 
> API Gateway : URL이 다다르므로 하나의 End-Point를 묶어서 단일화 해줘야됨 (로드밸런싱 , 라우팅,,인증..)


### 장단점

#### 장점 
- 독립 CI/CD관리가능
- 부분확장 관리 가능

#### 단점 
- 모노리틱보다 속도가 느림
- 통신에 사용하기 위해 값을 계속 데이터모델로 변환 => 그만큼 오버헤드가 발생
- 하나가 고장나면 전체 영향
- 만약 데이터 특성을 여러개 쓴다면.. 필자의 경우 대피소 재난서비스를 하는데 뉴스기사 크롤링은 NO-SQL // 대피소정보는 RDBMS가 나앗지만.. 혼용하기 어려워서 NOSQL로 통일함.
