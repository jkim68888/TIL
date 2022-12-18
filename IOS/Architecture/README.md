# ios 아키텍쳐 패턴 (IOS Architecture)

<div align="right">2022.12.18</div>

## 클린 아키텍쳐 (Clean Architecture)

<img width="597" alt="clean architecture" src="https://user-images.githubusercontent.com/75922558/208272602-7d3d4dd8-1415-41f6-878b-1f3337c5d3fc.png">
<div>사진 출처 : http://blog.cleancoder.com/uncle-bob/2012/08/13/the-clean-architecture.html</div>

<br/>

### 특징

1. 위 그림의 원에서 외부 영역과 내부 영역으로 나눠서 볼 수 있다. 이때, 외부 원에 있는 것들은 내부 원들에 영향을 미치지 않는다.
2. 원에서 화살표 방향으로 의존성 규칙이 향한다. 외부 영역은 내부 영역에 의존할 수 있지만, 그 반대의 경우는 성립할 수 없다.
3. 클린아키텍쳐를 구현하려면 세가지 레이어로 분리해야한다. (도메인 레이어, 데이터 레이어, 프리젠테이션 레이어)

<br/>

### 구조

1. 도메인 레이어 : Entity, Use Cases, Repositories Interfaces
2. 데이터 레이어 : Repositories, API Networking, DTO
3. 프리젠테이션 레이어 : ViewModels, Views

<br/>

### 용어

> Entity
> <br/>
> 서버의 데이터 원본

> UseCase
> <br/>
> 비즈니스 로직

> Controller
> <br/>
> 애플리케이션 API 엔드포인트

> Presenter
> <br/>
> 뷰와 이벤트 받는 역할

<br/>

### ViewModel의 역할

> 뷰모델은 UI이벤트가 발생하면 UseCase를 요청 후 View에 업데이트 알림 역할을 한다.

<br/>

## MVC 패턴

![Frame 26](https://user-images.githubusercontent.com/75922558/208272594-f57af6cb-2b18-4d14-a7e3-ded08c87825d.png)

<br/>

> 모델, 뷰, 컨트롤러로 구성되있다. 모델은 애플리케이션의 비즈니스 로직과 데이터들을 다룬다. 뷰는 사용자에게 보여지는 UI 영역이며 모델에 변경된 사항이 있으면 UI를 업데이트한다. 컨트롤러는 사용자에게 입력을 받거나 이벤트가 발생하면 로직에 맞게 모델을 가공한다.

<br/>

### 장점
- IOS UIKit에서 기본으로 제공하는 구조이다. 
- 구조가 단순해서 쉽고 빠르게 구현할 수 있다.

<br/>

### 단점
- 뷰와 모델의 의존성이 높다.
- 컨트롤러 안에 뷰가 존재해서 뷰를 변경하려면 컨트롤러를 변경해야 한다.
- 프로젝트 규모가 커지면 코드가 복잡해져서 유지보수가 어렵다.
- 컨트롤러가 특정 뷰와 모델에 의존적이여서 유닛테스트가 거의 불가능하다.

<br/>

## MVP 패턴

![Frame 27](https://user-images.githubusercontent.com/75922558/208272596-b4221db2-ba81-4a95-b917-92ba54f0a430.png)

<br/>

> MVP 패턴은 MVC패턴을 보완하여 생겨난 디자인 패턴으로 UI 로직과 비즈니스 로직을 분리하는데 집중한다.

<br/>

### 작동 방식
1. User input 이 View로 전달된다.
2. Presenter는 View에게서 입력을 전달받아 해당 입력에 맞는 Model을 업데이트 한다.
3. Model은 업데이트 된 데이터를 Presenter에 응답한다.
4. Presentor 가 데이터를 View에 응답한다.
5. View는 UI를 업데이트 한다.

<br/>

### 장점
- 모델과 뷰가 독립적이다.

<br/>

### 단점
- 프리젠터와 뷰 사이에 의존성을 가진다.

<br/>

## MVVM 패턴

![Frame 28](https://user-images.githubusercontent.com/75922558/208272597-3bd4a9c0-3ec5-49af-88ed-536c9f744fdd.png)

<br/>

> 뷰와 뷰모델은 1:n 대응하며, 뷰모델은 뷰에 보여주기 위한 데이터 처리를 수행한다. 뷰모델은 뷰에 값을 전달하는 것이 아닌, 뷰가 뷰모델을 관찰하며 뷰를 업데이트한다.

<br/>

### 작동 방식
1. User input 이 View로 전달된다.
2. View가 입력을 확인 후, ViewModel로 전달한다.
3. ViewModel이 Model에 데이터를 요청한다.
4. Model은 ViewModel에 데이터를 응답한다.
5. ViewModel은 데이터를 뷰에 보여줄 수 있는 형태로 가공하고 저장한다.
6. View는 ViewModel에 있는 가공된 데이터를 이용해서 UI를 업데이트 한다.

<br/>

### 장점
- 모델과 뷰 사이에 의존성이 없고, 뷰와 뷰모델 사이에도 의존성이 없다.
- 뷰와 뷰모델 사이의 결합도가 낮아 유닛테스트가 가능하다.
- ViewModel의 값이 변하면 View가 자동으로 업데이트 된다.
- 뷰는 뷰모델을 알고 있지만 뷰모델은 뷰를 알지 못하고, 뷰모델은 모델을 알지만 모델은 뷰모델을 알지 못한다. 즉, 한쪽 방향으로만 의존 관계가 있다.

<br/>

### 단점
- 구조 설계가 복잡하고 어렵다.

<br/>

### MVVM 패턴 구조의 흐름

![mvvm 구조 흐름](https://user-images.githubusercontent.com/75922558/208272761-7f83bed4-ae27-4831-b16c-b2de85825fcb.png)

> 의존성이 단방향으로 존재한다.

<br/>

### Entity와 Model의 용어 차이

- Entity : 서버에서 받아온 원본 데이터이다. (서버 데이터)
- Model : Entity를 통해 앱에서 실제로 사용될 데이터로 가공하여 만들어진 데이터이다. (앱에서 사용할 데이터)

<br/>

[MVVM과 클린아키텍쳐를 적용한 예시](https://github.com/jkim68888/bookSearch)