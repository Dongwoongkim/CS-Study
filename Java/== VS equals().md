
# ==

- 비교를 위한 연산자입니다.
- 비교하고자 하는 대상의 __주솟값__이 일치하는지 비교합니다.
- String의 경우 new 키워드로 생성하는 것이 아닌 리터럴을 사용하여 생성하는 경우, String pool을 이용하기 때문에 값이 같은 경우 같은 주솟값을 갖습니다.

> new 키워드의 경우 메모리 영역의 Heap 영역에 저장되어 사용JVM의 GC의 대상이 됨.

```java
String a = "hi";  
String b = "hi";  
String c = new String("hi");  
String d = new String("hi");  
  
System.out.println(a == b); // true  
System.out.println(a == c); // false  
System.out.println(c == d); // false
```

---

# equals()

- 객체의 내용(값)이 같은지 비교하는 메소드
- Wrapper 클래스의 값을 비교할 때 사용함.

```java
Integer a = 1;
Integer b = 2;
Integer c = 1;

System.out.println(a.equals(b)); // false;
System.out.println(a.equals(c)); // true;

```



