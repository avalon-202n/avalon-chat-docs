# 🅱 Backend


## Project Structure

### Overview

```
├─.github
│  └─workflows    # github action for ci & automated testing
├─avalon-chat-sub # git-submodule to store application.yml files
├─config          # external configuration - stores checkstyle/docker/...
└─src             
│   ├─main
│   │  ├─java     # a root of production code in java
│   │  │  └─com.avalon.avalonchat
│   │  │     ├─domain
│   │  │     │  ├─chat
│   │  │     │  ├─friend
│   │  │     │  ├─login
│   │  │     │  ├─model # a common model (baseXXXEntity) for domain 
│   │  │     │  ├─profile
│   │  │     │  └─user
│   │  │     ├─global
│   │  │     └─infra
│   │  └─resources
│   └─test
│       └─java
│           └─com.avalon.avalonchat
│              ├─domain
│              │  ├─chat
│              │  ├─friend
│              │  ├─login
│              │  ├─profile
│              │  └─user
│              ├─global
│              ├─infra
│              └─testsupport # utility classes for conveinient test
│
├─ docker-compose.yml # we use docker-compose for setup redis
└─ build.gradle.yml # we use gradle for build tool

```

- [패키지구조 레퍼런스](https://cheese10yun.github.io/spring-guide-directory/#-7)를 참고하여 상황에 맞게 커스텀하여 사용

### `domain`

- [도메인 주도 설계](https://ko.wikipedia.org/wiki/도메인_주도_설계)의 `도메인`을 의미한다.
	- `도메인` = 소프트웨어로 해결하고자 하는 문제영역 (이라는 추상적인 의미를 가진다)
- 각 `도메인` 패키지의 하위 패키지구조

```
└── friend   # aggregate root.
  ├── controller  # 
  ├── service     # 응용 서비스 계층 - 비즈니스 로직 수행
  ├── repository  # 리포지토리 
	 # 원칙상 하나의 aggregate root에 하나만 필요, 아래 도메인 패키지로 통합 필요
  ├── domain      # 도메인 - 도메인 엔티티/ 도메인 서비스/ (리포지토리)
  ├── dto         # 요청/응답 DTO, 컨트롤러/서비스 계층의 데이터 전달 모델
  └── exception   # 도메인 전용 예외 (e.g. LoginFailureException)
```

- 도메인의 핵심은 가능한 `POJO` 를 유지하는 것 스프링을 사용함에 따른 몇몇 의존성은 허용한다.

#### `controller`
- 역할 - 외부로 부터 요청을 받아 `응용 서비스`에게 처리를 위임, 응답을 받아 외부로 반환한다.
- `swagger-ui`를 활용한 api-documentation 생성을 위한 endpoint 정보를 제공 한다.

#### `(application) service`
- 역할 - 비즈니스 로직 처리/ 비즈니스 예외 검증
- 외부 시스템을 활용하는 경우 도메인 서비스/ 응용 서비스에 정의된 인터페이스를 이용해야 한다.
- `인터페이스`를 활용한다.

#### repository
- 역할 - 도메인 엔티티에 대한 CRUD 및 Join/ 필터링 등 간단한 처리를 적용한 조회 기능 제공
- `spring-data` 에 대한 의존을 허용한다.
- TODO - `domain.domain`으로 통합

#### `domain`
- 역할 
	- 가장 core 한 도메인 영역
	- `entity`는 JPA의 `@Entity` 의 역할도 수행한다.
- 많은 비즈니스 로직을 포함할 수 있도록 설계하면 좋다.
- 구분 - `entity`/`vo`/`domain-service`/`repository`

#### `dto`
- 역할 - 컨트롤러/서비스 계층의 매핑 모델
- 개발의 편의를 위해 두 계층에서 같은 모델을 활용한다.

#### `exception`
- 역할 - 도메인 전용 예외
- 정말 필요한지 고민해보고 도입하는 것을 추천한다.
	- 대부분의 경우 예외 메시지로 예외의 의미를 전달하기 충분한 경우가 많다.
	- global exception handler에 의해 다르게 처리가 될 필요가 있는경우에만 도입하자.
	- 구조적 complexity와 전용 클래스가 가지는 의미에 대한 trade-off 에대한 고민은 항상 중요하다! 

## Code Convention

- 기본적으로 `naver-hackday-convention` 및 `editorconfig` 를 활용한다.

### commons

- `final` 키워드는 활용하지 않는다.
- 애너테이션의 순서는 그 역할이 중요한 것이 아래로 가도록 한다. (가능하면?)
	- 롬복 애너테이션은 위로
	- `@Entity`, `@RestController`, `@Service` 와 같이 클래스의 핵심적인 역할을 드러내는 애너테이션은 아래로

#### comments

- 코드의 흐름을 나타내기 위해 `// 1. find profile` 과 같이 수행 동작을 순서와 함께 주석을 남긴다. 
- 클래스/인터페이스의 위에는 `javadoc` 스타일의 주석을 남긴다. 
	- html 태그 미활용
```java
/**
* 객체의 공통 매핑 정보
*/
@Getter ...
public abstract class BaseEntity {
	 ...
}
```

- 컨트롤러의 매핑 메서드에는 `swagger` 애너테이션으로 충분하므로 주석을 남기지 않는다.
- Service의 경우 인터페이스에 메서드의 역할을 javadoc 스타일의 주석을 남긴다.
	- 필요하다면 `@param`, `@return` 등의 키워드 활용
- 테스트 코드에는 bdd 스타일의 `// given // when //then` 주석 및 테스트 흐름 이해를 돕기 위한 주석을 포함한다. 예외를 검증하는 경우 `// when then` 을 한번에 작성한다.

### `domain.controller`

### `domain.service`

### `domain.dto`

### `domain.domain`

### `global.xxx`

### `infra.xxx`

### write test

## Exception Handling

### validation exception

### business logic exception

### how to use globally stored exception message

### how to configure exceptions on swagger-ui for specific endpoint

## naming rules - a.k.a ubiquitous language

```
TODO
```


## git/github

### branch strategy

- main
- dev
- feature/#xx

- branch protection on `dev` - requires at least `one approve`

### commit message

- free