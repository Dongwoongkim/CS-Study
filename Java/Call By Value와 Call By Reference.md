
Call by value, Call By reference. 이 둘은 함수/메소드에 매개변수를 전달하는 방식을 말합니다.

Call by value의 경우에는 "값"을 복사하여 전달하는 것을 말하고,
Call by reference의 경우에는 "주소 값"을 복사하여 전달하는 것을 말합니다.

Call by reference의 경우 Java나 C에서는 사용 불가. C++에서만 사용 가능

```cpp
// c++

int main() {
	int a,b;
  callByRef(a,b)
}

int callByRef(int &c, int &d) {
   c = 1;  // 매개 변수 c와 d를 위의 a, b와 동일하게 사용할 수 있다. 
   b = 2;  // main()의 a,b의 값이 변경된다.
}
```


### Primitive Type의 경우 Call By Value
ex) int, short, long, float, double 등

### Reference Type의 경우 Call By Reference
ex) Array, List 등

- 자바에서는 함수의 인자로 전달되는 타입이 원시타입인 경우 Value를 넘기게 되어 있음.

> 이 경우 메모리에는 함수를 위한 별도의 공간이 생성되고, 함수가 종료되면 함께 사라집니다.
>  쉽게 말해 Call by Value 방식을 수행할 때, 값을 넘겨받은 메소드에서  **값을 복사하여 새로운 지역 변수에 저장합니다**.
>  따라서 함수 내부에서 인자 값을 변경하더라도 원본 값이 바뀌지 않는 특징이 있습니다.


## Java에서 Call By Reference로 동작하는 것처럼 보이는 경우

```java
public static void main(String[] args) throws IOException {  
    int[] arr = {1, 2, 3};  
  
    for (int i : arr) {  
        System.out.println(i + " "); // 1 2 3  
    }  
  
    callByValue(arr);  
    for (int i : arr) {  
        System.out.println(i); // -1 2 3  
    }  
}  
  
private static void callByValue(int[] arr) {  
    arr[0] = -1;  
}
```

위 예시를 보면 array의 첫번째 값이 바뀐것을 볼 수 있습니다.
자바에서는 Call By Reference가 동작하지 않는다고 했는데 어떻게 된 것일까요??

위 코드를 보았을 때 매개변수로 reference를 준 것 처럼 보이지만, 변수가 가지는 값이 주소 값이기 때문에 Call by Value에 의해 주소 값이 전달되어 함수 안에서 해당 인자의 값을 변경하게 되면 주소값을 통해 참조하고 있는 값을 변경하기 때문에, 원본 Array도 변경된 것입니다.

arr의 reference를 넘겨주지 않았다는 것을 증명하기 위해 하나의 다른 예시를 살펴보며 마치겠습니다.

```java
public static void main(String[] args) throws IOException {  
    int[] arr = {1, 2, 3};  // 0x00
  
    for (int i : arr) {  
        System.out.println(i + " "); // 1 2 3  
    }  
  
    callByValue(arr);  
  
    for (int i : arr) {  
        System.out.println(i); // 1 2 3  
    }  
  
    System.out.println(arr[0]);  
}  
  
private static void callByValue(int[] arr) {  
	// Call by value 방식이므로 새로운 주소를 할당해도 변경되지 않음.  
    arr = new int[]{-1, -2, -3}; // 0x12
	// 0x12에 할당된 객체는 함수가 종료된 이후 GC에 의해 수거됨.
}
```




