### 23.1 소스코드의 타입
1. 전역 코드 : 전역에 존재하는 소스코드<br />
2. 함수 코드 : 함수 내부에 존재하는 소스코드<br />
3. eval 코드 : 빌트인 전역함수인 eval 함수에 인수로 전달되어 실행되는 소스코드<br />
4. 모듈 코드 : 모듈 내부에 존재하는 소스코드<br />
<br />
<br />
소스코드를 4가지 타입으로 구분하는 이유는 소스코드의 타입에 따라 실행 컨텍스트를 생성하는 과정과 관리 내용이 다르기 때문이다.

### 23.3 실행 컨텍스트의 역할
![context](https://github.com/user-attachments/assets/24a7d08c-d4aa-4545-ae21-326d1a856c47)

```js
// 전역 변수 선언
const x = 1;
const y = 2;

// 함수 정의
function foo(a) {
  // 지역 변수 선언
  const x = 10;
  const y = 20;

  // 메서드 호출
  console.log(a + x + y); // 130
}

// 함수 호출
foo(100);

// 메서드 호출
console.log(x + y); // 3
```