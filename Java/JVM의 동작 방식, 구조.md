
Java는 컴파일 방식과, 인터프리터 방식의 장점을 결합한 하이브리드 언어입니다.

![](https://blog.kakaocdn.net/dn/0wVtm/btsuQRG97iM/SFCzRjAggcjgobiyzCeCk1/img.png)

하이브리드 방식에서는 작성된 원시코드를 이진파일로 컴파일하는 과정과, 실제 해당 코드가 실행되는 시점(Runtime)에서 JVM에서 이 이진파일에서 필요한 부분들을 한 줄씩 읽어(interprete) 실행됩니다.

  

Runtime 시점에서 JVM을 통해 동작하여 자바는 운영체제로부터 독립적인 환경에서 실행 가능하다는 장점을 가지고 있습니다.

  
JVM이 내부에서 어떻게 동작하고 어떤 구조를 가지고 있는지 알아봅시다.

## JVM의 동작 방식과 구조 

![](https://blog.kakaocdn.net/dn/XDhrA/btsuZQ8lONg/TRKDPuKnwy3klFkGqZudK0/img.png)

  

1. 자바로 작성된 프로그램을 실행하면 JVM은 운영체제로부터 **메모리를 할당** 받습니다

-> 할당받은 영역 : Runtime Data Area 

> Runtime Data Area에는 "메소드 영역", "힙 영역", "스택 영역", "PC 레지스터 영역", "네이티브 메소드 스택 영역"으로 구분됨.
  

2. 자바 컴파일러가 자바 소스코드를 자바 바이트 코드(.class)로 컴파일

  

3. 이 바이트 코드 파일을 JVM 내부 Class Loader를 통해 Runtime Data Area로 로딩합니다.

- **Class Loader**
    - 자바는 실행 시점에 동적으로 클래스를 읽어오기 떄문에, 실행 시점에서 코드가 JVM과 연결됩니다. 이렇게 동적으로 클래스를 로딩해주는 역할을 하는 것이 바로 Class Loader.
    - Java에서 소스를 작성한 파일을 .java -> 실행 시점에 .java로 부터 필요한 코드를 뽑아온 이후 이진 파일로 변환된 .class 파일들을 적재하는 곳이 Class Loader

![](https://blog.kakaocdn.net/dn/lUnr3/btsu7R6tVsb/uk17XXiyn428wnOjHdWKEK/img.png)

- **Runtime Data Area**
    - 실행 시점에 사용하는 데이터들은 운영체제로부터 할당받은 메모리 영역인 Runtime Data Area에 메소드 영역, 힙 영역, 스택 영역, PC 레지스터, 네이티브 메소드 스택 5가지로 구분하여 적재합니다.
    - Class Loader에서 로드받은 .class 파일들을 메소드 영역에 저장.

4. Runtime Data Area에 로딩된 .class 파일들은 Excution Engine을 통해 해석합니다.

- **Execution Engine**
    - Runtime Data Area의 메소드 영역에 배치된 .class 파일들을 Execution Engine에 provide하여, 정의된 내용대로 바이트 코드를 실행시킵니다. (실제적으로 이진파일들이 실행되는 중요한 곳)

  

5. 해석된 바이트 코드는 Runtime Data Area의 각 영역에 배치되어 수행하며, 이 과정에서 Excution Engine에 의해 가비지 컬렉터가 동작하며, 스레드 동기화 또한 이루어집니다.

- **GC(Garbage Collector)**
    - 더 이상 사용하지 않는 메모리를 자동으로 회수해주는 역할
    - 이 덕분에 개발자는 별도로 사용하지 않는 메모리를 관리하지 않아도 됩니다.
    - 어떻게 동작하는가?
        - Heap 메모리 영역에 생성(적재)된 객체들 중에 참조되지 않은 객체들을 탐색 후 제거하는 역할을 하며 해당 역할을 하는 시간은 정확히 언제인지를 알 수 없습니다.

## Runtime Data Area의 각 영역에 어떤게 저장될까?

모든 Thraed가 공유하여 사용하는 공간

### 1. 메소드 영역 ( Method Area )

- 아까 언급했듯이 실행 시점에 사용되는 .class 파일들이 메소드 영역에 저장됩니다.
- 뿐만 아니라 클래스 멤버 변수의 이름, 데이터 타입, 접근 제어자 정보와 같이 각종 필드 정보들과 메소드 정보 데이터 Type 정보, static 변수, final class, 상수 풀 등이 이 곳에 저장됩니다.

  

### 2. 힙 영역 ( Heap Area )

![](https://blog.kakaocdn.net/dn/cA4Dv9/btsuQvxlS8p/1PUKO2vZSVWAhEx7QkYSE1/img.png)

- new 키워드로 생성된 객체, 배열이 저장되는 곳

- 효율적인 가비지 컬렉터 동작을 위해 힙 영역은 다시 3가지 영역으로 나뉩니다.
    - Young Generation : 객체가 생성되자마자 저장되고 생긴지 얼마 되지 않은 객체가 저장되는 공간.
    - Tenured Generation : Young Generation 공간이 꽉 찼을 때 새로운 객체나 배열이 생성되면 기존에 Young Generation에 있던 객체 및 배열의 참조가 이곳의 Old영역으로 이동되거나 회수됩니다. 
        - Young Generation과 Tenured Generation 에서의 GC를 "Minor GC"라고 한다.
    -  Old 영역에 할당된 메모리가 허용치를 넘게 되면, Old 영역에 있는 모든 객체들을 검사하여 참조되지 않는 객체들을 한꺼번에 삭제하는 GC가 실행됩니다. 
        - Old 영역의 메모리를 회수하는 GC를 Major GC라고 한다고 한다.

## 스레드마다 하나씩 생성되는 공간

### 1. 스택 영역 ( Stack Area ) 

- 지역변수, 파라미터 , 리턴 값, 연산에 사용되는 임시 값 등이 생성되는 영역

### 2. PC 레지스터

- 스레드가 생성될 떄마다 생성되는 영역으로, 현재 스레드가 실행되는 부분의 주소와 명령을 저장하고 있는 영역

### 3. 네이티브 메소드 스택 

- 자바 이외의 언어로 작성된 네이티브 코드를 실행할 때 메모리 영역으로 일반적인 C 스택을 사용
- 보통 C/C++ 코드를 수행하기 위한 스택

  