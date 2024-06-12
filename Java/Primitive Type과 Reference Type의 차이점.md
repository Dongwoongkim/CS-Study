자바에는 변수의 타입에 Primitive Type과 Reference Type이 있습니다.
Primitive Type을 "원시형, 기본형"이라 하며 Reference Type을 "참조형"이라고 합니다.

# 기본형/원시형 (Primitive Type)

- 기본형은 변수에 값 자체를 저장하며, 메모리 영역 중 stack 영역에 생성됩니다.
- 기본형 예시 : int, short, long 등 
- 사용하기 전 반드시 선언되어야 하며, 별도의 초기화 과정을 거치지 않는 경우 기본 값이 들어갑니다.

```java
public class Main {  
  
    static int i;  
    static short s;  
    static long l;  
    static double d;  
    static float f;  
    static char c;  
    static boolean b;  
  
    public static void main(String[] args) throws IOException {  
  
        System.out.println(i); // 0  
        System.out.println(s); // 0  
        System.out.println(l); // 0  
  
        System.out.println(d); // 0.0  
        System.out.println(f); // 0.0  
  
        System.out.println(c); // '\u0000' (null character)  
  
        System.out.println(b); // false  
    }  
}
```

- 비 객체 타입이기 때문에 절대 null 값을 가질 수 없습니다.


# 참조형 (Reference Type)

- 메모리 상에서 객체가 존재하는 "주소"를 저장하며, Heap 영역에 저장합니다.
- 
- 클래스형, 인터페이스형, 배열형이 있습니다.
	- 클래스형 : Integer, Long, Double, HashMap, ArrayList
	- 인터페이스형 : List, Map, Comparable 등
	- 배열형 : int[], char[], double[]