# [JS] "use strict" (2022-12-16)

</br>

## 1. 개요

자바스크립트의 발전은 기존의 기능을 변경하지 않으면서 새로운 기능만을 추가하여 발전하였다. </br>
즉 발전과정에서 호환성 이슈가 없었다. </br>

이말은 즉 기존에 작성된 코드에 영향을 주지 않는다. 단 언어가 만들어지는 과정에서 불완전한 문법 및 에러들을 개선 할 수 없다는 거울과 같은 단점이 존재한다. </br>

2009년 `ECMAScript5`가 등장하기 전까지 지속되었지만 새롭게 제정된 ES5에서 변화가 있었다. </br>

기능의 변경이 있었다. 하지만 하위 호환성 이슈를 대비하여 변경사항은 일반모드인 `느슨한 모드(sloppy mode)`에서는 활성화 되지 않게하여 호환성 이슈에 대비한 것이다.
그렇기에 변경사항은 `엄격모드(strict mode)`에서만 변경사항이 활성화 되도록 한 것 이다.

> 1. 오류를 발생시키도록 변경해 일부 자동 오류를 제거한다.
> 2. JS 엔진이 최적화 수행이 어렵게 하는 것을 수정한다. (동일한 코드를 빠르기 셀힝되도록 만들 수 있다.)
> 3. ECMAScript 향후 정의될 가능성 있는 일부 구문을 금지한다.

## 2. 호출

아래부턴 `엄격모드(strict mode)`는 `use strict` 으로 표기 할 것 이다.

```javascript
"use strict";

// 엄격모드(strict mode) 선언
```

`use strict`은 호출된 후 하위 소스코드에 적용된다. 즉 호출부 위에 작성된 코드에는 적용되지 않는다.

`use strict`은 스크립트 전체가 아닌 부분적으로도 적용 할 수 있다. </br>
함수 본문 맨 앞에 호출할 경우 해당 함수만 적용되어 활성화 된다.

> 단 간단한 매개변수가 있는 함수 본문에만 적용 할 수 있다. `rest`, `default`, `destructured` 매개변수 "use strict"와 함께 in 함수를 사용 하는 것은 `구문오류` 를 일으킨다. 이 점을 주의하자!

```javascript
function sum() {
  // OK
  "use strict"
  const a = 1;
  const b = 2;
  return a + b;
}

function sum(a = 1, b = 2) {
  // SyntaxError: "use strict" not allowed in function with default parameter
  "use strict";
  return a + b;
}
```

단 `use strict`은 대부분 스크립트 전체에 적용한다. </br>

부분적으로 필요할 경우도 있으나 작성 중 정말 필요한 부분에 선언을 누락할 수 있기 때문에 가능하다면 스크립트 `최상단`에 적용하는것을 권장한다.

> `use strict`을 취소할 방법은 존재하지 않는다.

</br>

## 3. 변경사항

`use strict`을 꼭 사용하여야 하는가? </br>

> 꼭 그런것만은 아니다.

모던 JS에는 `클래스` & `모듈`이 존재한다 이 둘의 구조에서는 `use strict`가 자동 적용된다. 즉 호출할 필요가 없다는 것 이다.

`use strict`는 구문과 런타임 동작 모두 변경시킨다.

1. 선언되지 않은 변수에 할당
   `use strict`는 전역 변수를 실수로 생성하는 것을 방지한다.
2. 개체 속성에 할당하지 못한다.
   `use strict`는 자동으로 예외를 `throw`하지 못하는 할당을 만든다.</br>
   속성 할당을 실패하는 경우는 3가지가 있다.

   > - `쓰기 불가능한` 데이터 속성 할당
   > - `getter` 전용 접근자 속성 할당
   > - `확장 불가한` 개체의 새 속성 할당

3. 개체 속성 삭제 실패
   구성할 수 없거난 삭제할 수 없는 속성에 삭제 시도시 `use strict` 발동된다.

이외 다양한 힝목이 있고, 이것은 참고자료로 확인하였던, [mdn](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Strict_mode)을 참고하길 바란다.
