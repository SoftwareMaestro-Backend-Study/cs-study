# [Java] JVM

## 1. JVM이란
JVM이란 Java Virtual Machine의 줄임말로 Java Byte Code를 OS에 맞게 해석해주는 역할을 한다.

> ### Java Byte Code
> 자바 가상 머신(JVM)이 이해할 수 있는 언어로 변환된 자바 소스 코드
> - 운영체제별로 프로그램을 실행하고 관리하는 방법이 다르기 때문에 운영체제와 자바 프로그램을 중계하는 JVM을 두어 자바 프로그램이 **여러 운영체제에서 동일한 실행 결과**가 나오게 한다.
> - Java Byte Code의 확장자는 .class

따라서 OS에 종속적이지 않고 Java 파일 하나만 만들면 어느 디바이스든 JVM 위에서 실행할 수 있다는 것이 Java의 큰 장점이다.

## 2. JVM 구성 요소
JVM은 크게 4가지 구성으로 나누어진다.
1. Class Loader
2. Execution Engine
3. Garbage Collector
4. Runtime Data Area

![](https://images.velog.io/images/minide/post/ae333858-7e81-42c0-b25a-19254a62bd05/%EC%8A%A4%ED%81%AC%EB%A6%B0%EC%83%B7%202021-01-07%20%EC%98%A4%ED%9B%84%204.50.54.png)
### 2-1. Class Loader
: Java 컴파일러에 의해 Byte Code로 변환된 클래스를 읽어들여 Runtime Data Area에 적재한다.
### 2-2. Execution Engine
: Class Loader에 의해 Runtime Data Area에 적재된 클래스(Byte Code)를 기계어로 변환하고 실행한다.
### 2-3. Garbage Collector
: Garbage Collector(GC)는 Heap 영역에 생성되어 있는 객체들 중 참조되지 않은 객체를 찾아 제거한다.
- GC가 실행되는 시간은 정해져 있지 않다. 특히 Full GC가 발생하는 경우, GC를 제외한 모든 스레드가 중지되기 때문에 장애가 발생할 수 있다.
### 2-4. Runtime Data Area
: JVM의 메모리 영역으로, Java 애플리케이션을 실행할 때 사용되는 데이터들을 적재한다.
- Method Area
  : 클래스 정보가 저장되는 공간
- Heap Area
  : new 키워드에 의해 생성되는 클래스와 배열 등이 저장되는 공간
- Stack Area
  : 지역 변수, 파라미터, 리턴 값, 연산에 사용되는 임시 값 등이 생성되는 영역
- PC Register
  : 스레드가 생성될 때마다 생성되며, 현재 실행 중인 주소와 명령을 저장하는 영역
- Native Method Stack
  : Java 이외의 코드(JNI)가 저장되는 공간

## 3. 컴파일하는 방법
terminal창에서 자바 코드를 실행해보기 위해 "hello, world!"를 출력하는 간단한 예제를 작성하였다.
먼저, javaTest파일이 존재하는 디렉토리로 이동해야하기 때문에 경로를 복사해준다.
![javaTest파일 경로 복사](https://images.velog.io/images/minide/post/13975e2e-4e0f-4842-8f79-373f27d266ec/%EC%8A%A4%ED%81%AC%EB%A6%B0%EC%83%B7%202021-01-07%20%EC%98%A4%ED%9B%84%2012.02.46.png)
> 복사한 파일 경로 : /Users/eojeong-yun/IdeaProjects/javastudy/src/main/java/javaTest.java

복사한 파일의 경로로 이동할때는 마지막에 있는 javaTest.java는 디렉토리가 아니기 때문에 지워야한다.
![디렉토리 이동 후 목록 보기](https://images.velog.io/images/minide/post/b59946eb-84ad-46d4-8fc9-65d28fcb4278/%EC%8A%A4%ED%81%AC%EB%A6%B0%EC%83%B7%202021-01-07%20%EC%98%A4%ED%9B%84%2012.04.00.png)
해당 디렉토리로 옮겨서 하위 목록을 보면 javaTest.java라는 파일이 하나 존재한다.
아래 코드를 입력해주고 다시 목록을 봤을 때 javaTest.class라는 파일이 생성됐으면 컴파일에 성공한 것이다.
```
$ javac 파일명.java
```
![컴파일 후 목록 보기](https://images.velog.io/images/minide/post/9b5a58f7-c8c6-4487-907f-eda547ad307e/%EC%8A%A4%ED%81%AC%EB%A6%B0%EC%83%B7%202021-01-07%20%EC%98%A4%ED%9B%84%2012.04.27.png)

## 4. 실행하는 방법
### 4-1. 컴파일한 후 실행하는 방법
디렉토리 하위 목록을 보면 .java 파일과 .class 파일이 있는 걸 알 수 있다.
![](https://images.velog.io/images/minide/post/9f19e25d-4caf-45ad-ad11-e08e792dad7f/%EC%8A%A4%ED%81%AC%EB%A6%B0%EC%83%B7%202021-01-07%20%EC%98%A4%ED%9B%84%2012.18.19.png)

아래 코드를 입력하면 코드가 실행된다.
```
$ java 파일명
```
![](https://images.velog.io/images/minide/post/4ceecf88-da0c-438b-9149-20c9a9ecfa2f/%EC%8A%A4%ED%81%AC%EB%A6%B0%EC%83%B7%202021-01-07%20%EC%98%A4%ED%9B%84%2012.17.54.png)

### 4-2. 컴파일하지 않고 실행하는 방법
컴파일을 하지 않았을 때도 자바 코드를 실행해볼 수 있다.
컴파일을 하지 않았을 때는 아래와 같이 Java Byte Code가 없다는 걸 확인할 수 있다.
![java 폴더 목록](https://images.velog.io/images/minide/post/a2b93a9f-7b1b-4296-93de-e2b755688ad0/%EC%8A%A4%ED%81%AC%EB%A6%B0%EC%83%B7%202021-01-07%20%EC%98%A4%ED%9B%84%2012.10.34.png)
이럴 때는 아래와 같이 코드 파일에 확장자명까지 추가해주면 된다.
```
$ java 파일명.java
```
![컴파일없이 자바 코드 실행](https://images.velog.io/images/minide/post/96f7e2dd-3c22-4add-a8e3-1b9e5af9754e/%EC%8A%A4%ED%81%AC%EB%A6%B0%EC%83%B7%202021-01-07%20%EC%98%A4%ED%9B%84%2012.10.51.png)

## 5. JIT 컴파일러
### 5-1. JIT 컴파일러란
JIT란 Just In Time의 약자로, JIT 컴파일러는 **프로그램을 실행하는 시점에(실시간으로) 기계어로 번역**하는 컴파일러이다.
- "한 번 작성하면 어디에서나 실행"이라는 자바의 장점의 핵심인 Byte Code는 애플리케이션에 대한 적절한 기본 명령어로 변환되는 방식에 따라 애플리케이션의 속도에 큰 영향을 미친다.
    - JVM의 표준 구현인 Byte Code로 해석하면 프로그램 실행 속도가 느려진다. 따라서 성능을 향상시키기 위해 JIT 컴파일러는 런타임에 JVM과 상호 작용하고 적절한 Byte Code 시퀀스를 반복적으로 해석하고 상대적으로 긴 변환 프로세스의 패널티를 초래하는 것과는 반대로 원시 코드를 실행할 수 있어 실행 속도의 성능 향상으로 이어질 수 있다.
    - 메소드가 덜 자주 실행되지 않는 한, JIT 컴파일러가 Byte Code를 컴파일하는 데 걸리는 시간은 전체 실행 시간에 추가되며, JIT에 의해 컴파일된 메소드가 자주 호출되지 않으면 Byte Code를 실행하는 인터프리터보다 실행 시간이 길어질 수 있다.
- JIT 컴파일러는 Byte Code를 Native Code로 컴파일할 때 특정 최적화를 수행한다. JIT 컴파일러는 일련의 Byte Code를 Native Code로 변환하므로 몇 가지 간단한 최적화를 수행할 수 있다.
    - JIT 컴파일러가 수행하는 일반적인 최적화 중 일부는 데이터 분석, 스택 작업에서 레지스터 작업으로의 변환, 레지스터 할당에 의한 메모리 액세스 감소, 공통 하위 표현식 제거 등이다.
    - JIT 컴파일러가 수행하는 최적화 수준이 높을 수록 실행 단계에서 더 많으 시간을 소비한다. 따라서 JIT 컴파일러는 실행 시간에 추가되는 오버 헤드와 프로그램에 대한 제한된 보기만 가지고 있기 때문에 정적 컴파일러가 수행하는 모든 최적화를 수행할 여유가 없다.

> JIT 컴파일러는 같은 코드를 매번 해석하지 않고 실행할 때 컴파일하면서 해당 코드를 캐싱해버린 후, 바뀐 부분만 컴파일하고 나머지는 캐싱된 코드를 사용한다.
**따라서, 인터프리터의 속도를 개선할 수 있다.**

### 5-2. JIT 동작 원리
JIT 컴파일러는 런타임 시 Java 애플리케이션의 성능을 향상시키는 JRE(Java Runtime Environment)의 구성요소이다. Java 프로그램은 Byte Code를 포함하는 클래스로 구성되는데, 런타임에 JVM은 클래스 파일을 로드하고 각 개별 Byte Code의 의미를 결정하고 적절한 계산을 수행한다. 해석 중 추가 프로세서 및 메모리 사용량은 Java 애플리케이션보다 느리게 수행됨을 의미한다. JIT 컴파일러는 런타임에 Byte Code를 Native Code로 컴파일하여 Java 프로그램의 성능을 향상시킨다.
![JIT 동작 원리](https://images.velog.io/images/minide/post/9bb05cd4-732d-471f-af94-8a1d21141ff6/%EC%8A%A4%ED%81%AC%EB%A6%B0%EC%83%B7%202021-01-07%20%EC%98%A4%ED%9B%84%204.30.17.png)

## 6. JDK와 JRE의 차이
- JDK(Java Development Kit)는 자바 개발 키트이다.
  JDK = JVM + 라이브러리 API + 컴파일러
- JRE(Java Runtime Environment)는 자바 실행 환경이다.
  JRE = JVM + 라이브러리 API

> 자바 프로그램을 개발하려면 JDK를 사용하면 되고, 개발된 프로그램을 실행만 한다면 JRE만 설치하면 된다.