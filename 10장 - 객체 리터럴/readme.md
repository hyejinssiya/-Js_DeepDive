### 10.1 객체란?
자바스크립트는 객체(object) 기반의 스크립트 언어이며 자바스크립트를 이루고 있는 거의 “모든 것”이 객체다. 
원시 타입(Primitives)을 제외한 나머지 값들(함수, 배열, 정규표현식 등)은 모두 객체.

자바스크립트의 객체는 키(key)과 값(value)으로 구성된 프로퍼티(Property)들의 집합.

이와 같이 객체는 데이터를 의미하는 프로퍼티(property)와 데이터를 참조하고 조작할 수 있는 동작(behavior)을 의미하는 메서드(method)로 구성된 집합. 
객체는 데이터(프로퍼티)와 그 데이터에 관련되는 동작(메서드)을 모두 포함할 수 있기 때문에 데이터와 동작을 하나의 단위로 구조화할 수 있어 유용하다.

### 10.2 객체 리터럴에 의한 객체 생성
가장 일반적인 자바스크립트의 객체 생성 방식.
중괄호({})를 사용하여 객체를 생성. 중괄호({})빈값일 경우, 빈객체 생성.

### 10.3 프로퍼티
프로퍼티는 키와 값으로 구성.

```js
var emptyObject = {};
console.log(typeof emptyObject); // object

var person = {
  name: 'Lee',
  gender: 'male',
  sayHello: function () {
    console.log('Hi! My name is ' + this.name);
  }
};

console.log(typeof person); // object
console.log(person); // {name: "Lee", gender: "male", sayHello: ƒ}

person.sayHello(); // Hi! My name is Lee
```
### 10.4 메서드
프로퍼티 값이 함수 일 경우 일반 함수와 구분하기 위해 메서드라 부름.

### 10.5 프로퍼티 접근
접근연산자 두가지 (마침표 표기법, 대괄호 표기법)

```js
var emptyObject = {};
console.log(typeof emptyObject); // object

var person = {
  name: 'Lee',
};

console.log(person.name); // Lee - 마침표 표기법
console.log(person['name']); // Lee - 대괄호 표기법
```

```js
var person = {
  'first-name': 'Ung-mo',
  'last-name': 'Lee',
  gender: 'male',
  1: 10
};

console.log(person);

console.log(person.first-name);    // NaN: undefined-undefined
console.log(person[first-name]);   // ReferenceError: first is not defined
console.log(person['first-name']); // 'Ung-mo'

console.log(person.gender);    // 'male'
console.log(person[gender]);   // ReferenceError: gender is not defined
console.log(person['gender']); // 'male'

console.log(person['1']); // 10
console.log(person[1]);   // 10 : person[1] -> person['1']
console.log(person.1);    // SyntaxError
```

person.last-name
Node.js의 환경에서는 ReferenceError: name is not defined 에러 발생 -> name이라는 식별자(변수, 함수 등의 이름)가 없기 때문
반면, 브라우저 환경에서는 Nan이 됨 -> name이라는 전역 변수가 암묵적으로 존재, 기본값은 빈값임. 따라서, undefinded-'' = Nan

### 10.8 프로퍼티 삭제
delete 연산자로 프로퍼티 삭제할 수 있다.

```js
var person = {
  name: 'Lee',
};
person.age = 20;

delete person.age; //age 프로퍼티 삭제
console.log(person); // {name: 'Lee'}
```

Object.defineProperty(person, 'age', {value: 20, configurable: false});
delete person.age 하더라도 삭제되지 않음

### 10.9 ES6에서 추가된 객체 리터럴의 확장 기능

프로퍼티 키 동적생성 비교

```js
//ES5 - 객체 리터럴 외부에서 생성
var perfix = 'prop';
var i = 0;

var obj = {};

obj[prefix + '-' + ++1] = i;
obj[prefix + '-' + ++1] = i;
obj[prefix + '-' + ++1] = i;
console.log(obj) // {prop-1: 1, prop-2: 2, prop-3: 3}

//ES6 - 객체 리터럴 내부에서 생성
const prefix = 'prop';
let i = 0;

const obj = {
    [`${prefix}-${++1}`]: i,
    [`${prefix}-${++1}`]: i,
    [`${prefix}-${++1}`]: i
};

console.log(obj) // {prop-1: 1, prop-2: 2, prop-3: 3}
```

메서드 축약 표현

```js
// ES5
var obj = {
  name: 'Lee',
  sayHi: function() {
    console.log('Hi! ' + this.name);
  }
};

obj.sayHi(); // Hi! Lee

// ES6
const obj = {
  name: 'Lee',
  // 메서드 축약 표현
  sayHi() {
    console.log('Hi! ' + this.name);
  }
};

obj.sayHi(); // Hi! Lee
```