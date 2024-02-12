## 테스트 코드란?

우리가 작성한 코드에 문제가 없는지 테스트하기 위해 작성하는 코드

**개발자가 작성한 코드를 실행하고 예상된 결과가 정상적으로 나오는지 확인**하는 데 사용된다.

## 테스트 코드 종류

![image](https://github.com/yu-heejin/jest-practice/assets/96467030/6fa90dcf-aa2a-4b66-a9b8-e221899ba0ab)


### 단위 테스트(Unit Test)

* **가장 작은 규모(함수)의 기능을 테스트**한다.

* **소프트웨어 개별 코드 단위를 테스트**하여 오류를 발견하고 이를 수정하여 전체적인 소프트웨어의 품질을 향상 시키는 과정이다.

### 통합 테스트(Integration Test)

* 여러가지 기능을 합쳤을 때 생기는 문제를 방지하기 위한 테스트

* 단위 테스트에서 **검증된 개별 모듈들을 결합하여 그들이 예상대로 상호작용하고 있는지 확인**하는 테스트

  * 예를 들어, 신규로 개발한 API 서버 내의 DB 호출 함수가 데이터베이스의 데이터를 잘 호출하고 있는지 테스트하는 과정을 의미한다.

* 일반적으로 모듈 간 인터페이스 테스트, 시스템 레벨 테스트 등의 방법으로 수행된다.

### E2E 테스트(End-to-End Test)

* 백엔드부터 시작해서 웹 페이지가 원하는대로 동작하며 원하는 데이터를 잘 보여주는지 확인하는 테스트

* 실제 사용자의 시나리오를 테스트함으로써 소프트웨어가 의도한대로 동작하는지 확인한다.

## 테스트 코드의 장단점

### 장점

* 테스트 코드를 통해 발생 가능성이 있는 오류를 사전에 찾아냄으로써 서비스의 품질을 향상시킬 수 있다.

* 테스트 코드 작성을 통해 다른 개발자가 작성한 코드의 예상 동작을 확인할 수 있어 문서화도 가능하다.

* 코드 수정 이후에도 기능이 정상적으로 작동하는 지 검증할 수 있다.

### 단점

* 테스트 코드를 작성하면서 발생하는 개발 시간 및 유지보수 비용이 발생한다.

* 서비스의 기능이 변경되거나 확장될 때마다 테스트 코드도 함께 수정해야한다.

* 테스트 코드에 많은 시간을 투자하다보면 오버 엔지니어링이 발생하기도 한다.

* 러닝 커브가 높은 편이라 학습하는데 시간이 필요하다.

## 테스트 코드 작성하기 with Jest

> Java에서 JUnit이 있다면, Javascript에는 jest가 있다.
> 

### Jest란?

* 페이스북에서 개발한 오픈 소스 자바스크립트 테스트 프레임워크이다.

* Jest 등장 이전에는 자바스크립트 코드를 테스트하기 위해 여러 테스팅 라이브러리를 조합해서 사용해야했지만, Jest의 등장 이후 Test Runner, Test Matcher, Test Mock 프레임워크까지 제공해주기 때문에 편리하게 테스트 코드를 작성할 수 있다.

### Jest 설치하기

```
npm i -D jest
```

- devDependencies로 설치해야 한다.

### Jest 기본 문법

> 파일명 기본 컨벤션은 `${testFileName}.test.js` *이다.*
> 

```jsx
describe('3 더하기 5의 결과는 무엇일까?', () => {
	test('3 더하기 5는 8입니다.', () => {
		expect(3 + 5).toEqual(8);
	}
}
```

* `describe`: 테스트 그룹을 묶어주는 역할을 한다.

  - 만약 test 함수가 위 예제처럼 하나라면 생략해도 괜찮다.
  - describe 옆 문자열에 어떤 코드를 테스트 하는지 설명을 작성할 수 있다.

* `test`: 테스트를 수행할 코드에게서 기대하는 값을 입력한다.

  - test 함수에도 어떤 코드를 테스트 하는지 설명을 작성할 수 있다.

* `expect`: 검증해야 할 코드를 해당 함수의 인수로 입력한다.

* `toEqual()`: Test Matcher 부분으로. expect의 결과가 해당 함수의 인수와 같은지 확인한다.

* 테스트 실행 결과는 다음과 같다.

  ![image](https://github.com/yu-heejin/jest-practice/assets/96467030/881bd7ae-73bc-4d75-9a90-9c6247fae44b)


### 자주 사용하는 Matcher

* `toEqual()`

  - 일반적으로 가장 많이 사용하는 함수
  - Test Matcher 부분으로. 검증 대상의 결과가 해당 함수의 매개변수와 같은지 확인한다.

* `toBeTruthy()`, `toBeFalsy()`

  - `toBeTruthy()`는 검증 대상의 결과가 true이면 테스트를 통과한다.
  - `toBeFalsy()`는 반대로 검증 대상의 결과가 false이면 테스트를 통과한다.

* `toHaveLength()`, `toContain()`

  - 배열의 길이를 체크하거나 특정 원소가 존재하는지 여부를 확인하는 경우 사용한다.
  - `toHaveLength()`는 배열의 길이를 체크할 때 쓰인다.
  - `toContain()`은 특정 원소가 배열에 들어 있는지를 테스트할 때 사용한다.

* `toThrow()`

  - 예외 발생 여부를 테스트해야할 때 사용한다.
  - 인자에 문자열을 넘기면 예외 메세지를 비교하고, 정규식을 넘기면 정규식을 체크한다.
  - `toThrow()`를 사용할 때 주의해야할 점이 있는데, `expect()` 함수에 넘기는 **검증 대상을 함수로 한번 감싸줘야한다.**
  - 그렇지 않으면 예외 발생 여부를 체크하는 것이 아니라 **테스트 실행 도중 정말 그 예외가 발생하기 때문에 그 테스트는 항상 실패하게 된다.**

## Jest 실습 해보기

### users 배열에서 ‘Neo’라는 닉네임을 가진 유저의 인덱스 위치 반환 테스트 작성

```jsx
// users 배열에서 'Neo'라는 닉네임을 가진 유저의 인덱스 위치 반환 테스트 작성
test('Neo라는 사람은 존재합니다.', () => {
    expect(findUser('Neo', users)).toEqual(0);
});
```

### users 배열에서 ‘Foo’라는 사람이 존재하지 않는지 확인

```jsx
// users 배열에서 'Foo'라는 사람이 존재하지 않는지 확인
test('Foo라는 사람은 없습니다.', () => {
 expect(findUserReturnBoolean('Foo', users)).toBeFalsy();
});
```

### (테스트 2개) 0으로 나누었을 때 오류가 발생하는지 확인, 4 나누기 2의 몫이 2인지 확인

```jsx
describe('나누기 함수 실행하기', () => {
 test('4 나누기 2는 2입니다.', () => {
  expect(calculateDivide(4, 2)).toEqual(2);
 });

 test('0으로 나누었을 때 오류가 발생합니다.', () => {
  expect(() => calculateDivide(3, 0)).toThrow('[ERROR] 나누는 수는 0이 될 수 없습니다.');
 });
});
```

## jest 환경 설정 시 주의사항

jest는 ES6 구문을 지원하지 않으며, 아래와 같은 오류가 발생한다.

```
Details:

.../jest-practice/__tests__/index.test.js:1
({"Object.<anonymous>":function(module,exports,require,__dirname,__filename,jest){import { findUser, findUserReturnBoolean, calculateDivide } from '../index';
```

ES6 문법을 설정하기 위해 아래 패키지를 추가로 설치하고, babel.config.js를 정의해야한다.

```
"@babel/core": "^7.23.2",
"@babel/preset-env": "^7.23.2",
"babel-jest": "^29.7.0",
```

```
// babel.config.js
module.exports = {
    "presets": ["@babel/preset-env"]
}
```

```
// jest.config.js
module.exports = {
    moduleFileExtensions: ["js", "json", "jsx", "ts", "tsx", "json"],
    transform: {
        '^.+\\.(js|jsx)?$': 'babel-jest'
    },
    testEnvironment: 'node',
    moduleNameMapper: {
        '^@/(.*)$': '<rootDir>/$1'
    },
    testMatch: [
        '<rootDir>/**/*.test.(js|jsx|ts|tsx)', '<rootDir>/(tests/unit/**/*.spec.(js|jsx|ts|tsx)|**/__tests__/*.(js|jsx|ts|tsx))'
    ],
    transformIgnorePatterns: ['<rootDir>/node_modules/']
};
```

## 참고 자료

- https://www.daleseo.com/jest-basic/
- [https://inpa.tistory.com/entry/JEST-📚-jest-문법-정리](https://inpa.tistory.com/entry/JEST-%F0%9F%93%9A-jest-%EB%AC%B8%EB%B2%95-%EC%A0%95%EB%A6%AC)
- [https://velog.io/@kon6443/Node-JS-Jest-supertest-개념-및-CRUD-API-testing-간단-예제](https://velog.io/@kon6443/Node-JS-Jest-supertest-%EA%B0%9C%EB%85%90-%EB%B0%8F-CRUD-API-testing-%EA%B0%84%EB%8B%A8-%EC%98%88%EC%A0%9C)
- https://yozm.wishket.com/magazine/detail/1964/
- https://www.startupcode.kr/company/blog/archives/17
- https://seungjuitmemo.tistory.com/269
