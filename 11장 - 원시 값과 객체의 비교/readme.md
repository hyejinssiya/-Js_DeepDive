### 11.1 원시 값
원시 값은 변경 불가능한 값, 즉 읽기 전용 값이므로 변경할 수 없다.
변수는 재할당이 가능하지만, 한번만 할당이 허용된 상수는 변수값을 변경(교체)할 수 없다.
ex) const

변수 선언을 하면 한 메모리 공간에 undefined 생성, var score === 0x000000F2
값을 할당하면 다른 메모리 공간에 값이 생기고, score = 80 === 0x00001332
재할당하면 또 다른 메모리 공간에 값이 생긴다. score = 90 === 0x0669f913

변수 값을 변경하기 위해 원시 값을 재할당하면 새로운 메모리 공간을 확보하고 재할당한 값을 저장한 후,
변수가 참조하던 메모리 공간의 주소를 변경한다. 이러한 특성을 불변성이라 한다.

*유사배결 객체
배열처럼 인덱스로 프로퍼티 값에 접근할 수 있고 length 프로퍼티를 갖는 객체.

```js
var str = 'string';

console.log(str[0]); // s

console.log(str.length); // 6
```
원시 값이지만 객체처럼 사용 가능 

```js
var str = 'string';

str[0] = 'S'

console.log(str); // string
```
문자열은 원시 값이므로 위 처럼 변경을 해도 변경되지 않음
재할당만 가능하다


값에 의한 전달

변수에는 값이 전달되는 것이 아니라 메모리 주소가 전달

```js
var score = 80;

// copy 변수에는 score 변수의 값 80이 복사되어 할당된다.
var copy = score;

console.log(score, copy);    // 80  80
console.log(score === copy); // true

// score 변수와 copy 변수의 값은 다른 메모리 공간에 저장된 별개의 값이다.
// 따라서 score 변수의 값을 변경해도 copy 변수의 값에는 어떠한 영향도 주지 않는다.
score = 100;

console.log(score, copy);    // 100  80
console.log(score === copy); // false
```

-> 다른 메모리 공간에 score 값이 복사되어 copy 값 생성
score값이 재할당되면 또 다른 메모리 공간에 값 생성

### 11.2 객체
객체는 변경 가능한 값이다. 
객체를 할당한 변수를 참조하면 메모리에 저장되어 있는 참조 값을 통해 실제 객체에 접근한다.

```js
// 할당이 이뤄지는 시점에 객체 리터럴이 해석되고, 그 결과 객체가 생성된다.
var person = {
  name: 'Lee'
};

// person 변수에 저장되어 있는 참조값으로 실제 객체에 접근해서 그 객체를 반환한다.
console.log(person); // {name: "Lee"}
```

객체는 여러개의 식별자가 하나의 객체를 공유할 수 있다.
객체의 프로퍼티 값을 변경하거나 하면 서로 영향을 받을 수 있는 부작용이 있다.

```js
var person = {
  name: 'Lee'
};

// 참조값을 복사(얕은 복사). copy와 person은 동일한 참조값을 갖는다.
var copy = person;

// copy와 person은 동일한 객체를 참조한다.
console.log(copy === person); // true

// copy를 통해 객체를 변경한다.
copy.name = 'Kim';

// person을 통해 객체를 변경한다.
person.address = 'Seoul';

// copy와 person은 동일한 객체를 가리킨다.
// 따라서 어느 한쪽에서 객체를 변경하면 서로 영향을 주고 받는다.
console.log(person); // {name: "Kim", address: "Seoul"}
console.log(copy);   // {name: "Kim", address: "Seoul"}
```

*얕은 복사와 깊은 복사
원시 값을 할당한 변수를 다른 변수에 할당하는 것을 깊은 복사,
객체를 할당한 변수를 다른 변수에 할당하는 것을 얕은 복사라고 한다.

```js
const o = { x: { y: 1 } };

// 얕은 복사
const c1 = { ...o }; // 35장 "스프레드 문법" 참고
console.log(c1 === o); // false
console.log(c1.x === o.x); // true

// lodash의 cloneDeep을 사용한 깊은 복사
// "npm install lodash"로 lodash를 설치한 후, Node.js 환경에서 실행
const _ = require('lodash');
// 깊은 복사
const c2 = _.cloneDeep(o);
console.log(c2 === o); // false
console.log(c2.x === o.x); // false
```