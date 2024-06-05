
- Java에서 Integer 타입의 값이 -128 ~ 127 인 경우 캐시를 가지고 있어서 해당 범위 안에존재하는 수에 대해서 String pool 처럼 같은 주솟값을 리턴합니다. 

```java
// case 1
Integer i1 = Integer.valueOf(127);
Integer i2 = Integer.valueOf(127);
System.out.println(i1 == i2); // true

// case 2
Integer i1 = Integer.valueOf(128);  
Integer i2 = Integer.valueOf(128);
System.out.println(i1 == i2); // false
```
