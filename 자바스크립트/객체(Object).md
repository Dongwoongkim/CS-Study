

---

## 1. 객체

객체형 타입을 제외한 나머지 7가지 타입들은 하나의 변수에 하나의 데이터만 담을 수 있었습니다. 이런 유형들을 **원시(primitive) 타입**이라 부릅니다. 하지만 객체형은 다릅니다. 하나의 변수에 다양한 데이터를 담을 수 있습니다. 객체 타입에는 key로 구분된 데이터 집합이나 복잡한 개체를 저장할 수 있습니다. 자바스크립트를 잘 다루려면 이 객체를 잘 이해하고 있어야 합니다.

  

객체는 **중괄호 {}**를 사용해서 만들거나 **new Object()**를 통해 만들 수 있습니다. 

let user = new Object(); // '객체 생성자' 문법
let user = {};  // '객체 리터럴' 문법, 객체를 만들 때 주로 이 방법을 사용함

  

중괄호 안에는 'key-value'쌍으로 구성된 프로퍼티를 여러 개 넣을 수 있는데, "key"에는 문자형, "value"에는 모든 자료형이 올 수 있습니다. (중괄호로 둘러싸인 객체형도 가능합니다.)

let user = {     // 객체
  name: "John",  // 키: "name",  값: "John"
  age: 30,        // 키: "age", 값: 30
  "likes birds" : true // 키 : likes birds, 값 : true
};

  

> 이 때 주의할 점으로는 세 번째 프로퍼티와 같이 공백글자가 포함된 key를 설정하고 싶다면 큰 따옴표로 묶을 수 있습니다.  
> 저러라고 만든 기능은 아닌 것 같네요. 하나의 예시일분 웬만하면 언더스코어 씁시다

  

외부에서 객체 프로퍼티의 값을 가져오고 싶다면 어떻게 하면 될까요? 자바처럼 점 표기법(dot notation)을 이용하면 프로퍼티 값을 읽을 수 있습니다. 유효한 변수 식별자가 아닌 경우엔 점 표기법 대신 **대괄호 표기법**을 사용하면 됩니다.

// 프로퍼티 값 얻기
alert( user.name ); // John
alert( user.age ); // 30

alert( user.full name ); // error
alert(user["full name"]);

  

객체에 프로퍼티를 추가하고 싶다면 어떻게 해야 할까요? 그냥 추가하면 됩니다. 

user.isAdmin = true;
user["likes birds"] = true;

  

프로퍼티 삭제는요? delete 키워드를 사용하면 됩니다. 쉽네요

delete user.age;
delete user["likes birds"];

  

### 대괄호 표기법

대괄호 표기법을 사용하면 모든 표현식의 평가 결과를 프로퍼티 키로 사용할 수 있습니다.

let key = "likes birds";

// user["likes birds"] = true; 와 같습니다.
user[key] = true;

  

변수 key는 런타임에 평가되기 때문에 사용자 입력값 변경 등에 따라 값이 변경될 수 있습니다. 어떤 경우든, 평가가 끝난 이후의 결과가 프로퍼티 키로 사용됩니다. 이를 응용하면 코드를 유연하게 작성할 수 있습니다.

let user = {
  name: "John",
  age: 30
};

let key = prompt("사용자의 어떤 정보를 얻고 싶으신가요?", "name");

// 변수로 접근
alert( user[key] ); // John (프롬프트 창에 "name"을 입력한 경우)

  

하지만 아래와 같이 **점 표기법**으로는 이런 방식이 불가능합니다. 

let user = {
  name: "John",
  age: 30
};

let key = "name";
alert( user.key ) // undefined

  

### 계산된 프로퍼티

이렇게 프로퍼티 키를 대괄호로 둘러싸는 경우 이를 **"계산된 프로퍼티"** 라고 부르는데요. 반대로 이렇게 사용할 수도 있습니다.

let fruit = prompt("어떤 과일을 구매하시겠습니까?", "apple");

let bag = {
  [fruit]: 5, // 변수 fruit에서 프로퍼티 이름을 동적으로 받아 옵니다.
};

alert( bag.apple ); // fruit에 "apple"이 할당되었다면, 5가 출력됩니다.

  

대괄호 표기법은 프로퍼티 이름과 값의 제약을 없애주기 때문에 점 표기법보다 훨씬 강력합니다. 그런데 작성하기 번거롭다는 단점이 있습니다. 이런 이유로 프로퍼티 이름이 확정된 상황이고, 단순한 이름이라면 처음엔 점 표기법을 사용하다가 뭔가 복잡한 상황이 발생했을 때 대괄호 표기법으로 바꾸는 경우가 많다고 합니다.

  

### 단축 프로퍼티

실무에선 프로퍼티 값을 기존 변수에서 받아와 사용하는 경우가 있습니다.

function makeUser(name, age) {
  return {
    name: name,
    age: age,
    // ...등등
  };
}

let user = makeUser("John", 30);
alert(user.name); // John

위 코드에서는 함수를 통해 객체를 생성하고, 점 표기법으로 프로퍼티 값을 가져오고 있습니다. 눈여겨봐야 할 점은 매개변수 이름과 프로퍼티 키 이름이 동일하다는 점인데요. 이러한 경우 더 짧게 줄일 수 있습니다. 아래 코드는 위와 동일하게 동작합니다.

function makeUser(name, age) {
  return {
    name, // name: name 과 같음
    age,  // age: age 와 같음
    // ...
  };
}

  

한 객체에서 일반 프로퍼티와 단축 프로퍼티를 동시에 사용하는 것도 가능합니다.

let user = {
  name,  // name: name 과 같음
  age: 30
};

  

### 프로퍼티 이름에는 제약 사항이 없다. 

변수명에는 예약어는 사용할 수 없었습니다. 제약사항이 있었습니다죠. 프로퍼티 이름은 다릅니다. 예약어를 사용할 수 있어요.

// 예약어를 키로 사용해도 괜찮습니다.
let obj = {
  for: 1,
  let: 2,
  return: 3
};

alert( obj.for + obj.let + obj.return );  // 6

- 예약어 뿐만 아니라 숫자형 값, 문자형 값, 심볼형 값(뒤에서 다룰 예정)도 프로퍼티의 키가 될 수 있습니다.
- 숫자형 값을 프로퍼티 키로 설정하는 경우 문자열로 자동변환 됩니다. 0 -> "0"
    - alert( obj["0"] ); // test
    - alert( obj[0] ); // test (동일한 프로퍼티)

이와같이 객체 프로퍼티 키에 쓸 수 있는 문자열엔 제약이 없지만, 역사적인 이유 때문에 특별 대우를 받는 이름이 하나 있습니다.

  

**바로, __proto__입니다.**

let obj = {};
obj.__proto__ = 5; // 숫자를 할당합니다.
alert(obj.__proto__); // [object Object] - 숫자를 할당했지만 값은 객체가 되었습니다. 의도한대로 동작하지 않네요.

  

> __proto__의 본질은 "프로토타입 상속"에서, 이 문제를 어떻게 해결할 수 있을지에 대해선 프로토타입 메서드와 __proto__가 없는 객체에서 자세히 다룰 예정입니다.

  

### ‘in’ 연산자로 프로퍼티 존재 여부 확인하기

자바스크립트가 자바와 다른점은 객체에 찾고자 하는 프로퍼티가 존재하지 않는 경우 에러가 발생하지 않고 **"undefined를 리턴"**한다는 점인데요. 이런 특징을 살려 프로퍼티 **존재 여부를 쉽게 확인**할 수 있습니다.

alert( user.noSuchProperty === undefined ); // true는 '프로퍼티가 존재하지 않음'을 의미합니다.

위처럼 확인할 수도 있지만 in 연산자를 사용하여 확인할 수도 있습니다.

let user = { name: "John", age: 30 };

/**
이 때 반드시 
1. in 왼쪽엔 프로퍼티 이름을 문자열로 감싸야 합니다.
2. 
*/
alert( "age" in user ); // user.age가 존재하므로 true가 출력됩니다.
alert( "blabla" in user ); // user.blabla는 존재하지 않기 때문에 false가 출력됩니다.

  

== undefined로 확인하는 것과 in으로 확인하는 것은 무슨 차이가 있을까요?

만약 아래와 같이 프로퍼티는 존재하는데, 값에 undefined가 할당된 경우를 생각해보면 **in을 쓰는 것이 프로퍼티 존재여부를 확인하기에 더 적합하다는 것을 느끼실 수 있으실 겁니다.**

let obj = {
  test: undefined
};

alert( obj.test == undefined ); // 값이 `undefined`이므로, true. 
// 하지만 존재여부로 판단한 것이 아니라 test 프로퍼티의 값이 undefined인 것으로 판단한 것이므로 정확하지 X

alert( "test" in obj ); // `in`을 사용하면 프로퍼티 유무를 제대로 확인할 수 있습니다(true가 출력됨).

  

### for...in 반복문

for..in 반복문을 사용하면 객체의 모든 키를 순회할 수 있습니다. for..in은 for(;;) 반복문과는 완전히 다릅니다.

  

let user = {
  name: "John",
  age: 30,
  isAdmin: true
};

for (let key in user) {
  // 키
  alert( key );  // name, age, isAdmin
  // 키에 해당하는 값
  alert( user[key] ); // John, 30, true
}

  

### 번외 : 프로퍼티에는 순서가 있을까?

객체는 특별한 방식으로 정렬됩니다. 정수 프로퍼티는 오름차순으로 자동으로 정렬되고 그 외의 프로퍼티는 객체에 **추가한 순서 그대로** 정렬됩니다. 자세한 내용은 예제를 통해 살펴봅시다.

- 참고로 **정수 프로퍼티**란 문자열->숫자형, 숫자형->문자열로 값의 변형없이 왔다갔다 할 수 있는 프로퍼티를 말함.
    - alert( String(Math.trunc(Number("49"))) ); // '49'가 출력. 기존에 입력한 값과 같으므로 정수 프로퍼티임.
    - alert( String(Math.trunc(Number("+49"))) ); // '49'가 출력. 기존에 입력한 값(+49)과 다르므로 정수 프로퍼티가 님
    - alert( String(Math.trunc(Number("1.2"))) ); // '1'이 출력. 기존에 입력한 값(1.2)과 다르므로 정수 프로퍼티가 아님

let codes = {
  "49": "독일",
  "41": "스위스",
  "44": "영국",
  // ..,
  "+1": "미국"
};

for (let code in codes) {
  alert(code); // 41, 44, 49, 1
}

let user = {
  name: "John",
  surname: "Smith"
};
user.age = 25; // 프로퍼티를 하나 추가합니다.

// 정수 프로퍼티가 아닌 프로퍼티는 추가된 순서대로 나열됩니다.
for (let prop in user) {
  alert( prop ); // name, surname, age
}

  

### 번외 : 상수 객체의 프로퍼티를 수정할 수 있을까?

const user = {
  name: "John"
};

user.name = "Pete"; // (*)

alert(user.name); // Pete

- const는 user의 값을 고정한 것이지, 그게 user의 프로퍼티를 고정한 것을 의미하지는 않습니다.
- 따라서 user = ~~;와 같이 'user' 그 자체를 변경하려고 하는 경우에는 에러가 발생하지만, 객체의 프로퍼티를 건든다고 해서 에러가 발생하지는 않습니다.

  

---

## 2. 참조에 의한 객체 복사

자바 스크립트에서 원시타입은 call by value, 객체타입은 call by reference 방식으로 동작합니다.

  

즉, 원시타입의 경우 복사했을 경우 "값" 자체가 복사되므로 값의 변경이 이루어진다고 해서 복사된 객체까지 변경되진 않는다는 말입니다. 아래가 그 예시입니다.

let a = 1;
let b = a;

console.log(a); // 1
console.log(b); // 1

a = 2;
console.log(a); // 2
console.log(b); // 1

  

반면, 객체는 call by reference 방식이기 때문에 "주소"가 복사되는 방식으로 복사가 이루어져, 원본객체가 바뀐다면 복사객체도 바뀌게 됩니다.

  

let a = {
    name : 'kim'
}

let b = a;

console.log(a.name); // kim
console.log(b.name); // kim

a.name = 'park';
console.log(a); // park
console.log(b); // park

  

### 객체 복사, 병합, Object.assign

그렇다면 객체를 독립된 객체로 복제하고 싶다면 어떻게 해야 할까요? 객체를 독립된 객체로 복사하는 방법은 있습니다만, 꽤나 복잡합니다. 그럴 일도 잘 없구요.

  

#### iterate하여 key 복사

let user = {
  name: "John",
  age: 30
};

let clone = {}; // 새로운 빈 객체

// 빈 객체에 user 프로퍼티 전부를 복사해 넣습니다.
for (let key in user) {
  clone[key] = user[key];
}

// 이제 clone은 완전히 독립적인 복제본이 되었습니다.
clone.name = "Pete"; // clone의 데이터를 변경합니다.

alert( user.name ); // 기존 객체에는 여전히 John이 있습니다.

  

#### Object.assgin 사용

Object.assign(dest, [src1, src2, src3...])

- 첫 번째 인수 dest는 **복사될 객체**입니다.
- 이어지는 인수 src1, ..., srcN는 **복사하고자 하는 객체**입니다. ...은 필요에 따라 얼마든지 많은 객체를 인수로 사용할 수 있다는 것을 나타냅니다.

_사용 예시_

let user = { name: "John" };

let permissions1 = { canView: true };
let permissions2 = { canEdit: true };

// permissions1과 permissions2의 프로퍼티를 user로 복사합니다.
Object.assign(user, permissions1, permissions2);

// now user = { name: "John", canView: true, canEdit: true }

  

그런데 만약 아래와 같이 객체의 프로퍼티에 객체가 포함되어 있다면 어떻게 될까요?

let user = {
    name: "John",
    sizes: {
        height: 182,
        width: 50
      }
};

let k = {};
Object.assign(k, user);

user.sizes.height = 10;
console.log(k.sizes.height); // 10

이 경우에는 sizes 프로퍼티는 객체형이기 때문에 call by reference로 복사가 이루어집니다. 즉, user의 sizes에 변경이 일어나면 k의 sizes에도 동일하게 변경이 일어나게 되죠.

  

이 문제를 해결하기 위해서는 1번 방법을 사용하여 각 값을 검사하면서 그 값이 객체인 경우 객체의 구조도 call by value로 복사해주는 **"깊은 복사"** 방식을 사용해야 합니다.

  

#### _.cloneDeep(obj) 

자바스크립트 라이브러리 lodash의 메서드인 _.cloneDeep(obj)을 사용하면 이 알고리즘을 직접 구현하지 않고도 **깊은 복사**를 처할 수 있습니다.

let _ = require('lodash');

let user = {
    name: "John",
    sizes: {
        height: 182,
        width: 50
      }
};

let k = _.cloneDeep(user);
user.sizes.height = 100;
console.log(k.sizes.height); // 182

---

## 3. 가비지 컬렉션

자바와 마찬가지로 자바스크립트에서도 가비지 컬렉터가 동작합니다. Java는 주로 서버나 엔터프라이즈 애플리케이션 환경에서 동작하며, JVM을 통한 세대별 메모리 관리 및 가비지 컬렉션 기법을 적용합니다. 반면 JavaScript는 브라우저나 Node.js와 같은 비동기 환경에서 동작하며, 비교적 간단한 가비지 컬렉션 기법을 사용합니다.

  

JS에서는 "도달 가능성"이라는 개념을 사용해 메모리 관리를 수행합니다. "도달 가능하다"는 값은 쉽게 말해 어떻게든 접근이 가능한 값을 의미하는데, 이 경우에는 메모리에서 삭제되지 않습니다. 

  

아래 값들은 태생부터 "도달 가능한 값"들이기 때문에 메모리에서 삭제되지 않는다는 점을 기억합시다.

- 현재 함수의 지역변수와 매개변수
- 중첩 함수의 체인에 있는 함수에서 사용되는 매개변수, 변수
- 전역 변수 

이런 값들은 "root"라고 부릅니다. 

  

그렇다면 "도달할 수 없는" 값은 무엇일까요? 예시로 살펴봅시다.

// user엔 객체 참조 값이 저장됩니다.
let user = {
  name: "John"
};

user = null;

// 자, 이제 "John"은 도달할 수 없는 상태가 되었습니다.

  

user에 null 값을 할당하는 순간부터는 user.name에 접근할 도리가 없습니다. user을 복사한 것이 아니라면요. "도달할 수 없다"는 의미가 이해가 되셨나요? 

  

JS에서는 루트 정보를 수집하고 이를 mark(기억)하며, 주기적으로 루트가 참조하고 있는 모든 객체들 또한 방문하고 이것들을 mark합니다. mark된 객체들이 참조하는 객체들도 mark 합니다. 이렇게 도달 가능한 모든 객체들을 **각 한번씩 방문(방문했던 객체를 다시 mark하는 경우는 없음)**하며, 객체가 여전히 사용 중인지 확인하기 위해 객체를 '마크'하고, 사용되지 않는 객체는 '스윕' 과정을 통해 메모리를 정리합니다.  

  

이런 방식을 Mark-And-Sweep 방식이라 부릅니다.

  

가비지 컬렉션에 대해 더 자세히 알아보고 싶으시다면 아래 링크를 참고하시면 좋을 것 같습니다.

[

  

가비지 컬렉션

  

ko.javascript.info



](https://ko.javascript.info/garbage-collection)

---

## 4. 메소드와 this

JS에서도 당연히 객체에도 메소드를 만들 수 있습니다.

let user = {
    name: "John",
    age: 30,
    bye : function() {
        console.log(this.name + " : 안녕히 계세요.");
    }
  };
  
  user.sayHi = function() {
    console.log("안녕하세요!");
  };

  user.sayHi();
  user.bye();

  

### 메소드 단축 구문

객체 리터럴 안에 메소드를 선언할때 사용할 수 있는 단축 문법입니다.

// 아래 두 객체는 동일하게 동작합니다.

user = {
  sayHi: function() {
    alert("Hello");
  }
};

// 단축 구문을 사용하니 더 깔끔해 보이네요.
user = {
  sayHi() { // "sayHi: function()"과 동일합니다.
    alert("Hello");
  }
};

  

일반적인 방법과 단축 구문을 사용한 방법이 완전히 동일하진 않습니다. 객체 상속과 관련된 미묘한 차이가 존재하는데 지금으로선 이 차이가 중요하지 않기 때문에 넘어가도록 하겠습니다.

  

### this

메서드 내부에서 this 키워드를 사용하면 객체에 접근할 수 있습니다. 이 때 점 앞의 this는 객체를 나타냅니다. 정확히는 메서드를 호출할 때 사용된 객체를 나타내죠.

let user = {
  name: "John",
  age: 30,

  sayHi() {
    // 'this'는 '현재 객체'를 나타냅니다.
    alert(this.name);
  }

};

user.sayHi(); // John

  

user.sayHi()가 실행되는 동안에 this는 user를 나타냅니다.  
this를 사용하지 않고 외부 변수를 참조해 객체에 접근하는 것도 가능합니다.

let user = {
  name: "John",
  age: 30,

  sayHi() {
    alert( user.name ); // Error: Cannot read property 'name' of null
  }

};

let admin = user;
user = null; // user를 null로 덮어씁니다.

admin.sayHi(); // sayHi()가 엉뚱한 객체를 참고하면서 에러가 발생했습니다.

  

그런데 이렇게 외부 변수를 사용해 객체를 참조하면 예상치 못한 에러가 발생할 수 있습니다. user를 복사해 다른 변수에 할당(admin = user)하고, user는 전혀 다른 값으로 덮어썼다고 가정해 봅시다. sayHi()는 원치 않는 값(null)을 참조할 겁니다. user.name대신 this.name을 인수로 받았다면 에러가 발생하지 않겠죠.

  

자바스크립트에서 this는 다른 언어의 this와 동작방식이 조금 다릅니다. **자바스크립트에서는 모든 함수에 this를 사용할 수 있습니다.** 즉, 아래처럼 작성해도 에러가 발생하지 않습니다.

function sayHi() {
  alert( this.name );
}

  

this 값은 런타임에 결정됩니다. 즉, 동일한 함수라도 **다른 객체에서 호출했다면** this가 가리키는 값이 달리지게 됩니다.

let user = { name: "John" };
let admin = { name: "Admin" };

function sayHi() {
  alert( this.name );
}

// 별개의 객체에서 동일한 함수를 사용함
user.f = sayHi;
admin.f = sayHi;

// 'this'는 '점(.) 앞의' 객체를 참조하기 때문에
// this 값이 달라짐
user.f(); // John  (this == user)
admin.f(); // Admin  (this == admin)

admin['f'](); // Admin (점과 대괄호는 동일하게 동작함)

  

객체가 없어도 함수를 호출할 수 있습니다. strict mode라면 undefined가 할당되고, strict mode가 아닐 때에는 this는 window라는 전역 객체를 참조합니다. 따라서 이런 식의 코드는 대개 실수로 작성된 경우가 많습니다. 만약 함수 본문에 this가 사용되었다면, 객체 컨텍스트 내에서 함수를 호출할 것이라고 예상하시면 됩니다.

function sayHi() {
  alert(this);
}

sayHi(); // undefined

'use strict';
function sayBye() {
	console.log(this);
}

sayBye();
/**
ref *1> Object [global] {
  global: [Circular *1],
  clearImmediate: [Function: clearImmediate],
  setImmediate: [Function: setImmediate] {
    [Symbol(nodejs.util.promisify.custom)]: [Getter]
  },
  clearInterval: [Function: clearInterval],
  clearTimeout: [Function: clearTimeout],
  setInterval: [Function: setInterval],
  setTimeout: [Function: setTimeout] {
    [Symbol(nodejs.util.promisify.custom)]: [Getter]
  },
  queueMicrotask: [Function: queueMicrotask],
  structuredClone: [Function: structuredClone],
  atob: [Getter/Setter],
  btoa: [Getter/Setter],
  performance: [Getter/Setter],
  fetch: [Function: fetch],
  crypto: [Getter]
}
*/

  

### this가 없는 화살표 함수

화살표 함수는 일반 함수와는 달리 ‘고유한’ this를 가지지 않습니다. 화살표 함수에서 this를 참조하면, 화살표 함수가 아닌 ‘평범한’ 외부 함수에서 this 값을 가져옵니다.  
  
아래 예시에서 함수 arrow()의 this는 외부 함수 user.sayHi()의 this가 됩니다.

let user = {
  firstName: "보라",
  sayHi() {
    let arrow = () => alert(this.firstName);
    arrow();
  }
};

user.sayHi(); // 보라

  
별개의 this가 만들어지는 건 원하지 않고, 외부 컨텍스트에 있는 this를 이용하고 싶은 경우 화살표 함수가 유용합니다. 이에 대한 자세한 내용은 별도의 챕터, 화살표 함수 다시 살펴보기에서 다루겠습니다.

---

## 5. new 연산자와 생성자 함수

중괄호 객체 리터럴 ({...})를 사용하면 객체를.쉽게 만들 수 있습니다. 뿐만 아니라 new 키워드와 함수를 통해서 객체를 만들 수도 있는데요. 그 방법을 알바봅시다.

### 생성자 함수

"일반 함수"와 구분되는 "생성자 함수"라는 것이 있습니다. 기술적인 차이는 없고, 두 관례를 따를 뿐입니다.

1. 함수의 첫 글자는 대문자로.
2. 반드시 "new" 연산자를 앞에 붙여 실행

예시를 보겠습니다.

function User(name) {
	this.name = name;
    this.isAdmin = false;
}

let user = new User("보라");

alert(user.name); // 보라
alert(user.isAdmin); // false

  

new User(...)를 써서 함수를 실행하면 암시적으로 다음과 같이 동작합니다.

// 암시적으로 아래와 같이 동작함.
function User(name) {
  // this = {};  (빈 객체가 암시적으로 만들어짐)

  // 새로운 프로퍼티를 this에 추가함
  this.name = name;
  this.isAdmin = false;

  // return this;  (this가 암시적으로 반환됨)
}

  

1. 빈 객체를 만들어 this에 할당

2. 함수 본문 실행. (this에 새로운 프로퍼티를 추가해 this 수정)

3. this return

  

생성자 함수가 재사용 가능성이 없다면, 익명함수로 이렇게 만들 수도 있겠습니다. 한 번만 사용한다면 재사용을 막으면서 코드를 캡슐화 할 수 있습니다.

let user = new function() {
  this.name = "John";
  this.isAdmin = false;

  // 사용자 객체를 만들기 위한 여러 코드.
  // 지역 변수, 복잡한 로직, 구문 등의
  // 다양한 코드가 여기에 들어갑니다.
};

  

### new.target과 생성자 함수

new.target 프로퍼티를 사용하면 함수가 new와 함께 호출되었는지 아닌지 알 수 있습니다.

- new 키워드와 함께 호출된 경우 : 함수 자체를 return
- new 키워드 없이 호출된 경우 : undefined retrurn

function User() {
    console.log(new.target);
}

User(); // undefined

new User(); // [Function: User]

  

new.target은 어떻게 사용할 수 있을까요? 바로 이를 활용해 new 키워드 없이도 new 키워드를 붙여 생성자 함수를 호출한 것처럼 동작하게 할 수 있겠습니다. 

function User(name) {
    if(!new.target) {
        return new User(name);
    }

    this.name = name;
}

let userA = User("a");
let userB = new User("b");

console.log(userA.name); // a
console.log(userB.name); // b

  

이런 방식을 사용하면 new를 붙여 함수를 호출하든 아니든 코드가 동일하게 동작하기 때문에, 좀 더 유연하게 코드를 작성할 수 있습니다. new를 생략해서 객체를 만들 일이 있을 지 모르겠지만, 만약 있다면 위 코드처럼 사용하면 되겠네요.

  

### 생성자와 return문

반환해야 할 것들은 모두 this에 저장되고, this는 자동으로 반환되기 때문에 반환문을 명시적으로 써 줄 필요가 없습니다. 따라서 생성자함수엔 보통 return 문이 없습니다. 만약 return 문이 있다면 어떻게 동작할까요?

- return 원시형 : 무시됨
- return 객체 : this 대신 객체가 반환됨.

function BigUser() {
  this.name = "원숭이";
  return { name: "고릴라" };  // <-- this가 아닌 새로운 객체를 반환함
}

alert( new BigUser().name );  // 고릴라

function SmallUser() {
  this.name = "원숭이";
  return; // <-- this를 반환함
}

alert( new SmallUser().name );  // 원숭이

  

### 생성자 내 메소드

생성자 함수를 사용하면 매개변수를 이용해 객체 내부를 자유롭게 구성할 수 있습니다. 엄청난 유연성이 확보되죠.  
지금까진 this에 프로퍼티를 더해주는 예시만 살펴봤는데, 메소드를 더해주는 것도 가능합니다.  
아래 예시에서 new User(name)는 프로퍼티 name과 메서드 sayHi를 가진 객체를 만들어줍니다.

function User(name) {
  this.name = name;

  this.sayHi = function() {
    alert( "제 이름은 " + this.name + "입니다." );
  };
}

let bora = new User("이보라");

bora.sayHi(); // 제 이름은 이보라입니다.

/*
bora = {
   name: "이보라",
   sayHi: function() { ... }
}
*/

---

## 6. 옵셔널 체이닝 '?.'

옵셔널 체이닝 "?."을 사용하면 프로퍼티가 "없는" 중첩 객체를 에러없이 안전하게 접근할 수 있습니다. 

예전 JS에서는 체이닝된 객체의 특정 프로퍼티에 접근하기 위해서는 항생 AND로 연결해서 실제 해당 객체나 프로퍼티가 있는지 먼저 확인 하는 방법을 사용했었습니다.

// 예시
alert( obj && obj.obj2 && obj.obj2.obj3 && obj.obj2.obj3.property )

  

이렇게 AND로 연결하면 코드가 길어진다는 단점을 해결해주는 것이 바로 옵셔널 체이닝 "?."입니다.

?.은 ?.'앞’의 평가 대상이 **undefined나 null**이면 평가를 멈추고 **undefined**를 반환합니다. 이 때 반드시 '앞'의 평가 대상은 존재해야 합니다. 쉽게말해,  '앞'의 평가 대상은 변수로서 선언 되어 있어야 합니다. (그렇지 않으면 오류남)

let user = { 
	name : {
        containsA : false,
    }
};

undefined?.name // undefined 
null?.name // undefined
user?.name // kim
user.name?.containsA // false

// user가 null 또는 undefined가 아니고 실제 값이 존재하는 경우에는
// 반드시 user.address 프로퍼티는 있어야 합니다.
// 그렇지 않으면 user?.address.street의 두 번째 점 연산자에서 에러가 발생
// 이를 활용한다면 ?.로 계속 연결해서 중첩 프로퍼티들에 안전하게 접근할 수 있음.
user?.address.street // error : address prop is not exist.

  

이 외에도 "?."는 또 다른 형태로 사용할 수 있습니다. 대표적으로 ?.[prop], ?.method() 가 있습니다.

- obj?.prop – obj가 존재하면 obj.prop을 반환하고, 그렇지 않으면 undefined를 반환함.
- obj?.[prop] – obj가 존재하면 obj[prop]을 반환하고, 그렇지 않으면 undefined를 반환함.
- obj?.method() – obj가 존재하면 obj.method()를 **호출**하고, 그렇지 않으면 undefined를 반환함.

---

## 7. Symbol

JS는 객체의 프로퍼티 키로 오직 문자형과 심볼형만을 허용합니다. 

let obj = {};
obj[true] // error
obj[undefined] // error
obj[1] // error
obj[null] // error

지금까지는 프로퍼티 키가 문자형인 경우만 살펴보았습니다. 이번에는 프로퍼티 키로 심볼값을 사용해보면서 이점을 알아보겠습니다.

  

심볼은 "유일 식별자"를 만들고자 할 때 유용합니다.

심볼값은 Symbol()을 사용해 만들 수 있습니다.

let k = Symbol("k");

심볼은 유일성을 보장하는 "자료형"이기 때문에 이름이 동일한 심볼이라고 해서 각 심볼이 같지 않습니다.

let id1 = Symbol("id");
let id2 = Symbol("id");

console.log(id1 == id2); // false

  

자바스크립트에선 문자형으로의 암시적 형 변환이 비교적 자유롭게 일어나는 편입니다. alert 함수가 거의 모든 값을 인자로 받을 수 있는 이유가 이 때문이죠. 그러나 심볼은 예외입니다. 심볼형 값은 다른 자료형으로 암시적 형 변환(자동 형 변환)되지 않습니다.  
  
아래 예시에서 alert는 에러를 발생시킵니다.

let id = Symbol("id");
console.log(id); // error

- 보시는 것처럼 문자열과 심볼은 근본부터 다르기 때문에 서로의 타입으로 변환해서는 안됩니다. 만약 반드시 출력해야 하는 상황이라면 .toString() 메소드를 호출하거나 심볼의 .description 프로퍼티를 이용할 수 있겠습니다.

### '숨김' 프로퍼티

심볼을 사용하면 숨김 프로퍼티를 만들 수 있습니다. 숨김 처리를 통해 외부 코드에서 접근 및 변경이 불가능하도록 만드는 것이죠. 예시를 통해 숨김 프로퍼티를 만들어 봅시다.

let user = { 
	name: "John"
};

let id = Symbol("id");

user[id] = 1;

alert( user[id] ); // 심볼을 키로 사용해 데이터에 접근할 수 있습니다.

  

user 객체가 서드파티로부터 가져와 새로운 프로퍼티를 추가할 수 없는 상황이라 가정해봅시다.

이 때 심볼을 사용한다면 서드파티 코드에서 접근할 수 없기 때문에, 서드파티 코드가 모르게 user에 식별자를 부여할 수 있습니다.

심볼은 유일성이 보장되므로 우리가 만든 식별자와 제3의 스크립트에서 만든 식별자가 충돌하지 않습니다. 이름이 같더라도 말이죠.

let user = { name: "John" };

// 문자열 "id"를 사용해 식별자를 만들었습니다.
user.id = "스크립트 id 값";

// 만약 제3의 스크립트가 우리 스크립트와 동일하게 문자열 "id"를 이용해 식별자를 만들었다면...

user.id = "제3 스크립트 id 값"
// 의도치 않게 값이 덮어 쓰여서 우리가 만든 식별자는 무의미해집니다.

  
만약 심볼 대신 문자열 "id"를 사용해 식별자를 만들었다면 기존 값과의 충돌이 발생할 가능성이 있습니다. 이것이 바로 심볼을 사용하는 이유입니다.

> 또한 심볼은 for in에서도 배제되어 심볼 그 자체로 숨김 프로퍼티의 기능을 가지고 있습니다.  
> 뿐만 아니라 Object.keys(user)에서도 키가 심볼인 프로퍼티는 배제됩니다. '심볼형 프로퍼티 숨기기(hiding symbolic property)'라 불리는 이런 원칙 덕분에 외부 스크립트나 라이브러리는 심볼형 키를 가진 프로퍼티에 접근하지 못합니다.

  

But, Object.assgin은 키가 심볼인 프로퍼티를 포함한 모든 프로퍼티를 복사합니다.

let id = Symbol("id");
let user = {
  [id]: 123
};

let clone = Object.assign({}, user);

alert( clone[id] ); // 123

  

추가로 객체를 생성하고 난 후에 심볼을 추가하기보다, 객체 생성 과정에서 심볼을 프로퍼티로 넣고 싶다면 [] 대괄호를 사용하면 됩니다.

let id = Symbol("id");

let user = {
  name: "John",
  [id]: 123 // "id": 123은 안됨
};

  

### Symbol.for() - 전역 심볼 생성

// 전역 레지스트리에서 심볼을 읽습니다.
let id = Symbol.for("id"); // 만약 "id"이름의 심볼이 전역 레지스트리에 존재하지 않으면 새로운 심볼을 만듭니다.

// 동일한 이름을 이용해 심볼을 다시 읽습니다(좀 더 멀리 떨어진 코드에서도 가능합니다).
let idAgain = Symbol.for("id");

// 두 심볼은 같습니다.
alert( id === idAgain ); // true

  

애플리케이션에서 광범위하게 사용해야 하는 심볼이라면 전역 심볼을 사용하면 되겠습니다.

  

### Symbol.keyFor() - 전역 심볼의 이름 get

Symbol.for과 반대로 심볼을 이용해 심볼의 이름을 get할 수 있는 함수가 바로 keyFor()입니다.

// 이름을 이용해 심볼을 찾음
let sym = Symbol.for("name");
let sym2 = Symbol.for("id");

// 심볼을 이용해 이름을 얻음
alert( Symbol.keyFor(sym) ); // name
alert( Symbol.keyFor(sym2) ); // id

  

전역 심볼이 아닌 모든 심볼은 description 프로퍼티가 있습니다. 만약 전역심볼이 아닌 일반 심볼에서 이름을 얻고 싶으면 description 프로퍼티를 사용하면 됩니다.

let localSymbol = Symbol("name");
alert( localSymbol.description ); // name

  

### 시스템 심볼

'시스템 심볼(system symbol)'은 자바스크립트 내부에서 사용되는 심볼입니다. 시스템 심볼을 활용하면 객체를 미세 조정할 수 있습니다.

- Symbol.hasInstance, Symbol.isConcatSpreadable, Symbol.iterator, Symbol.toPrimitive 기타 등등

---

## 8.  객체를 원시형으로 변환

JS에서는 객체를 형변환하는 경우 "hint"라고 하는 기준 값에 의해 형변환이 일어납니다. 예를 들어 객체를 console로 출력하려 한다고 해봅시다. 이 경우에는이 "hint"에 의해 자동으로 string으로 형변환이 일어납니다. hint의 종류에는 string, number, default 총 3가지가 있습니다.

  

하나씩 알아봅시다.

  

### string

let user = { 
    name : 'kim'
};

console.log(user); // string으로 형변환

  

console.log 메소드는 매개변수로 오는 객체들을 string으로 변환하여 콘솔에 출력합니다. 객체를 원시형으로 변환하는 과정에서 "hint"가 **string**이 됩니다.

  

### number

객체간 연산을 시도하는 경우 객체의 hint는 **number**가 됩니다.

const people = {
    age: 24,
    name: 'James'
}

const now = Date.now();
const someday = new Date('2024-09-27');

const num = +people; // 객체 -> 숫자형 변환
const day = now - someday; // 두 날짜간의 차이

console.log(num, day); // NaN, 93788797

  

### default

연산자가 기대하는 자료형이 확실하지 않을 때는 'hint'가 default 가 됩니다. 이항 덧셈 연산자 + 는 피연산자의 자료형에 따라 "문자열을 합치는 연산"을 할 수도, "숫자를 더해주는 연산"을 할 수도 있습니다. 따라서 +의 인수가 "객체"일 떄는 hint가 default가 됩낟.

  

뿐만 아니라 동등연산자 == 또한 객체-문자형, 객체-숫자형, 객체-심볼형끼리 비교할 때도 객체를 어떤 자료형으로 바꿔야 할 지 명확하지 않으므로 hint 가 default 가 됩니다.

// 이항 덧셈 연산은 hint로 `default`를 사용합니다.
let total = obj1 + obj2;

// obj == number 연산은 hint로 `default`를 사용합니다.
if (user == 1) { ... };

>   
> "boolean" hint는 없습니다.  
> hint는 총 세 가지입니다. 아주 간단하죠.‘boolean’ hint는 존재하지 않습니다.  
> 모든 객체는 그냥 true로 평가됩니다.

  

  

### Symbol.toPrimitive

자바스크립트엔 Symbol.toPrimitive라는 내장 심볼이 존재하는데, 이 심볼은 아래와 같이 목표로 하는 자료형(hint)을 내 입맛대로 다룰 수 있습니다. 

let user = {
    name : 'John',
    money : 10000,
    
    [Symbol.toPrimitive](hint) {
        console.log(`hint: ${hint}`);
        return hint == "string" ? `{name: "${this.name}"}` : this.money;
    }
}

console.log(user); // hint 가 string이므로 return {name: ${this.name}} 
console.log(+user); // hint 가 string이 아니므로 return this.money
console.log(user + 500); // hint 가 string이 아니므로 return this.money

이렇게 메서드를 구현해 놓으면 user는 hint에 따라 (자기 자신을 설명해주는) 문자열로 변환되기도 하고 (가지고 있는 돈의 액수를 나타내는) 숫자로 변환되기도 합니다. user[Symbol.toPrimitive]를 사용하면 메서드 하나로 모든 종류의 형 변환을 다룰 수 있습니다.

  

### toString(), valueOf()

Symbol.toPrimitive을 사용하지 않고도 형변환 할 수 있습니다. 바로 toString()과 valueOf()를 사용해서 말이죠.

객체-원시형 변환은 다음과 같은 알고리즘에 의해 동작합니다.

  

객체에 Symbol.toPrimitive가 없으면 자바스크립트는 아래 규칙에 따라 toString이나 valueOf를 호출합니다.

- hint가 'string’인 경우: toString -> valueOf 순(toString이 있다면 toString을 호출, toString이 없다면 valueOf를 호출함)
- 그 외(number, default) : valueOf -> toString 순 호출 

따라서 이 hint가 string인 경우에는 toString(), number나 default인 경우에는 valueOf() 메소드에 어떻게 원시타입으로 변환할지 변환 방법을 작성하면 되겠습니다.

let user = {
  name: "John",
  money: 1000,

  // hint가 "string"인 경우
  toString() {
    return `{name: "${this.name}"}`;
  },

  // hint가 "number"나 "default"인 경우
  valueOf() {
    return this.money;
  }

};

alert(user); // toString -> {name: "John"}
alert(+user); // valueOf -> 1000
alert(user + 500); // valueOf -> 1500

  

간혹 모든 형 변환을 한 곳에서 처리해야 하는 경우 (hint가 number던 string이던 default던 상관없이 동일한 방식으로 변환하고자 하는 경우) 에는 toString()만 구현해주면 되겠습니다.

_(Symbol.toPrimitive와 valueOf가 모두 없으면 toString이 모든 형변환을 책임지기 때문이죠.)_

let user = {
  name: "John",

  toString() {
    return this.name;
  }
};

alert(user); // toString -> John
alert(user + 500); // toString -> John500

  

### 번외 : 추가 형변환

위와 같이 toString()만 작성한 경우 아래 코드는 각각 어떻게 동작할까요?

let obj = {
  toString() {
    return "2";
  }
};

alert(obj + 2); // (1)

let obj = {
  toString() {
    return "2";
  }
};

alert(obj * 2); // (2)

  

(1) : toString()은 기본적으로 hint가 'string'입니다. 따라서 문자열 병합을 우선순위로 두겠죠. 결과는 22입니다.

(2) : toString()에 의해 obj가 문자열 "2"가 됩니다. 그렇담 "2" * 2가 되고 이것은 다시 2 * 2로 변환되어 결과는 4가 되겠습니다.

  

사실 obj.toString()만 사용해도 '모든 변환’을 다 다룰 수 있기 때문에, 실무에선 obj.toString()만 구현해도 충분한 경우가 많습니다. 그렇지만 Symbol.toPrimitive로도 각 hint를 처리할 수 있다는 점. valueOf()로 number, default를 처리할 수 있다는 점을 기억합시다.

---

## 9. 프로퍼티 Flag와 설명자

지금까지는 프로퍼티를 단순히 key-value 관점에서만 다뤘습니다. 하지만 프로퍼티는 생각보다 더 유연하고 강력한 구조인데요.

이번에는 객체 프로퍼티 추가 구성 옵션 몇 가지를 알아보겠습니다.

  

### 프로퍼티 Flag

- **writable** : true 면 해당 프로퍼티의 값을 수정할 수 있습니다. false인 경우 읽기(get)만 가능합니다.
- **enumerable** : true 면 반복문을 사용해 나열할 수 있습니다. false인 경우 반복문에 포함되지 않습니다.
- **configurable** : true 면 프로퍼티 삭제나 플래그 수정이 가능합니다. false인 경우 삭제, 수정이 불가능합니다.

기본적으로 모든 flag는 default로 true로 설정되어 있습니다.

  

프로퍼티의 flag 정보는 [Object.getOwnPropertyDescriptor](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Object/getOwnPropertyDescriptor)메서드를 사용하면 특정 프로퍼티에 대한 정보를 모두 얻을 수 있습니다.

let descriptor = Object.getOwnPropertyDescriptor(obj, propertyName);

let user = {
  name: "John"
};

let descriptor = Object.getOwnPropertyDescriptor(user, 'name');

alert( JSON.stringify(descriptor, null, 2 ) );
/* property descriptor:
{
  "value": "John",
  "writable": true,
  "enumerable": true,
  "configurable": true
}
*/

  

메서드 [Object.defineProperty](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Object/defineProperty)를 사용하면 플래그를 변경할 수 있습니다.

let user = {
  name: "John"
};

Object.defineProperty(user, "name", {
  writable: false
});

  

[Object.defineProperties(obj, descriptors)](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Object/defineProperties) 메서드를 사용하면 프로퍼티 여러 개를 한 번에 정의할 수 있습니다.

Object.defineProperties(user, {
  name: { value: "John", writable: false },
  surname: { value: "Smith", writable: false },
  // ...
});

  

[Object.getOwnPropertyDescriptors(obj)](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Object/getOwnPropertyDescriptors) 메서드를 사용하면 프로퍼티 설명자를 전부 한꺼번에 가져올 수 있습니다.

이 메서드를 Object.defineProperties와 함께 사용하면 **객체 복사 시 플래그도 함께 복사할 수 있습니다. ( for문을 통해 깊은 복사를 한다고 해서 프로퍼티의 플래그까지 복사되지는 않습니다. )**

let clone = Object.defineProperties({}, Object.getOwnPropertyDescriptors(obj));

  

이 외에도 객체 수정을 막아주는 다양한 메소드들이 있습니다. 잘 사용되진 않기 때문에 이런게 있구나 정도로 보면 되겠습니다.

  

- **Object.preventExtensions(obj)**
    - 객체에 새로운 프로퍼티를 추가할 수 없게 합니다.
- **Object.seal(obj)**
    - 새로운 프로퍼티 추가나 기존 프로퍼티 삭제를 막아줍니다. 프로퍼티 전체에 configurable: false를 설정하는 것과 동일한 효과입니다.
- **Object.freeze(obj)**
    - 새로운 프로퍼티 추가나 기존 프로퍼티 삭제, 수정을 막아줍니다. 프로퍼티 전체에 configurable: false, writable: false를 설정하는 것과 동일한 효과입니다.

아래 메서드는 위 세 가지 메서드를 사용해서 설정한 제약사항을 확인할 때 사용할 수 있습니다.

- **Object.isExtensible(obj)**
    - 새로운 프로퍼티를 추가하는 게 불가능한 경우 false를, 그렇지 않은 경우 true를 반환합니다.
- **Object.isSealed(obj)**
    - 프로퍼티 추가, 삭제가 불가능하고 모든 프로퍼티가 configurable: false이면 true를 반환합니다.
- **Object.isFrozen(obj)**
    - 프로퍼티 추가, 삭제, 변경이 불가능하고 모든 프로퍼티가 configurable: false, writable: false이면 true를 반환합니다.

---

## 10. Getter & Setter

객체의 프로퍼티는 크게 두 종류로 나뉩니다.

- 데이터 프로퍼티 : 지금까지 사용한 key-value 쌍의 데이터. 이 데이터 프로퍼티를 조작하는 프로퍼티 flag를 위에서 다루었음.
- 접근자 프로퍼티 : getter와 setter.

JS에서 Getter와 Setter는 get과 set으로 나타낼 수 있습니다.

let user = {
    name : 'kim',
    get name() {
        ...
    },

    set name(value) {
        ...
    }
};

getter 메소드는 user.name을 사용해 프로퍼티를 읽으려고 할 때 실행되고, setter 메소드는 user.name = value로 프로퍼티에 값을 할당하려 할 때 실행됩니다.

console.log(user.name); //  name Getter 실행
user.name = 'park'; // name Setter 실행

  

그렇다면 get과 set은 객체가 가지고 있는 프로퍼티에 대해서만 생성할 수 있을까요? 그렇지 않습니다.

아래처럼 getter와 setter 메서드를 구현하면 객체엔 fullName이라는 '가상’의 프로퍼티가 생깁니다. 가상의 프로퍼티는 읽고 쓸 순 있지만 실제로는 존재하지 않습니다.

let user = {
  name: "John",
  surname: "Smith",

  get fullName() {
    return `${this.name} ${this.surname}`;
  }
};

alert(user.fullName); // John Smith
user.fullName = "Test"; // Error (프로퍼티에 getter 메서드만 있어서 에러가 발생합니다.)

  

## Getter & Setter 설명자

접근자 프로퍼티인 getter, setter에도 프로퍼티 flag가 있습니다.

데이터 프로퍼티 flag의 value와 writable이 없는 대신 get과 set이라는 함수가 있습니다.

  

- get – 인수가 없는 함수로, 프로퍼티를 읽을 때 동작함
- set – 인수가 하나인 함수로, 프로퍼티에 값을 쓸 때 호출됨
- enumerable – 데이터 프로퍼티와 동일함
- configurable – 데이터 프로퍼티와 동일

따라서 아래와 같이 defineProperty에 설명자 get과 set을 전달하면 fullName을 위한 접근자를 만들 수 있습니다.

let user = {
  name: "John",
  surname: "Smith"
};

Object.defineProperty(user, 'fullName', {
  get() {
    return `${this.name} ${this.surname}`;
  },

  set(value) {
    [this.name, this.surname] = value.split(" ");
  }
});

alert(user.fullName); // John Smith

for(let key in user) alert(key); // name, surname

  

주의할 점으로는 프로퍼티는 **접근자 프로퍼티(get/set 메서드를 가짐)**나 **데이터 프로퍼티(value를 가짐)** 중 한 종류에만 속하고 둘 다에 속할 수 없다는 점을 항상 유의하시기 바랍니다.  
  
따라서 한 프로퍼티에 get과 value를 동시에 설정하면 에러가 발생합니다.

// Error: Invalid property descriptor.
Object.defineProperty({}, 'prop', {
  get() {
    return 1
  },

  value: 2
});

  

### getter, setter 활용하기

getter, setter를 활용하여 프로퍼티의 값을 원하는대로 통제할 수 있습니다.

let user = {
  get name() {
    return this._name;
  },

  set name(value) {
    if (value.length < 4) {
      alert("입력하신 값이 너무 짧습니다. 네 글자 이상으로 구성된 이름을 입력하세요.");
      return;
    }
    this._name = value;
  }
};

user.name = "Pete";
alert(user.name); // Pete

user.name = ""; // 너무 짧은 이름을 할당하려 함

  

user의 이름은 _name에 저장되고, 프로퍼티에 접근하는 것은 getter와 setter를 통해 이뤄집니다.  
  
기술적으론 외부 코드에서 user._name을 사용해 이름에 바로 접근할 수 있습니다. 

이 때 **밑줄 "_" 로 시작하는 프로퍼티는 객체 내부에서만 활용**하고, 외부에서는 건드리지 않는 것(getter한다거나 setter하지 않는 것)이 관습입니다.

  

## 접근자 프로퍼티를 활용하여 OCP 지키기

만약 아래와 같은 기존 코드가 존재할 때,

function User(name, age) {
  this.name = name;
  this.age = age;
}

let john = new User("John", 25);

alert( john.age ); // 25

  

age 프로퍼티 대신 birthday 프로퍼티를 가져야 한다는 요구사항의 변경이 일어났다고 가정해봅시다.

age 프로퍼티는 삭제하지 않아야 한다고 할 때, 코드를 어떻게 작성하면 좋을까요?

  

아래 코드가 그 정답입니다.

function User(name, birthday) {
    this.name = name;
    this.birthday = birthday;

    Object.defineProperty(this, 'age', {
        get() {
            let nowYear = new Date().getFullYear();
            return nowYear - this.birthday.getFullYear();
        },
    });
}

let john = new User('John', new Date(1992, 6, 1));

console.log(john.age);
console.log(john.birthday);

  

이제 기존 코드도 잘 작동하고, 프로퍼티도 생겼네요. 이렇게 접근자 프로퍼티를 잘 활용하면 코드를 변경하지 않고 확장하여 OCP를 지킬 수 있답니다.

---

이렇게 JS의 Object에 대해 알아보았습니다. 기존에 사용하던 OOP 언어와 비슷한 점도 많고, 새로운 점도 많은 것 같습니다.

  
특히 각각의 프로퍼티에 대해 Object.defineProperty()를 통해 getter와 setter를 제어한다는 점이 캡슐화 측면에서 Java와는 방식이 달라 흥미로웠습니다.

자바스크립트의 접근 방식은 보다 유연하고 세밀한 제어를 가능하게 하지만, 자바의 캡슐화는 private, protected, public 같은 접근 제어자를 사용해 클래스 내 멤버(필드, 메서드 등)의 접근 권한을 명확하게 제어하여 안정적이고 엄격한 데이터 보호를 제공하는 점에서 차이가 있는 것 같습니다.

  

다음 포스팅에서는 이어 객체와 관련 깊은 JS의 클래스에 대해 알아보겠습니다. 감사합니다.