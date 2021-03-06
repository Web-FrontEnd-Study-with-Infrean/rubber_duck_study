## 실행컨텍스트
실행컨텍스트는 자바스크립트의 핵심 동작과 개념을 이해하는데 있어 필수적으로 알고 있어야 하는 개념입니다. 실행컨텍스트의 동작을 이해하면 자바스크립트의 호이스팅이나 클로저 그리고 this, 스코프체인 등의 주요 개념들에 대해서 이해할 수 있고 코드의 실행 순서를 예측해 볼 수 있습니다.
  
실행컨텍스트는 소스코드가 실행되는 환경을 제공하고 코드의 실행순서가 결정되는 영역입니다. 이것은 자바스크립트 엔진에 의해서 처리되는 과정입니다. 실행컨텍스트의 실행단계는 준비단계, 초기화 단계, 코드실행단계로 나누어 볼 수 있습니다. 
  
실행컨텍스트가 생성되는 시점은 실행가능한 코드를 만났을때이고 이 시점은 크게 두가지로 나누어 볼 수 있습니다. 전역실행컨텍스트와 함수실행컨텍스트 입니다.
- 전역실행컨텍스트
- 함수실행컨텍스트

실행컨텍스트 시점이 나뉘는 이유는 내부에서의 처리방법과 실행환경이 다르기 떄문입니다. 글로벌코드는 전역환경에서 실행되고 함수코드는 렉시컬환경에서 실행됩니다.
  
실행컨텍스트는 상태 컴포넌트를 갖습니다.

- LexicalEnvironment (렉시컬 환경)
- VariableEnvironment (변수 환경)
- PrivateEnvironment (개별 환경) - 원래 this 바인딩 이었던것같은데 최근 문서에서는 변경된것같습니다.
  
해당 상태 컴포넌트들은 실행컨텍스트내의 프로퍼티이기때문에 해당 컴포넌트들도 객체라고 볼 수 있습니다.
  
렉시컬환경에서는 식별자를 해결할 수 있습니다. 그리고 함수가 중첩되어있을때 외부함수와 그 외부함수의 함수와 변수를 참조하는 환경이기도합니다. 렉시컬환경 컴포넌트생성은 function, with, try-catch 에서 생성됩니다. 렉시컬환경은 환경레코드와 외부 렉시컬 환경참조로 구성되어있습니다. 환경레코드에 함수와 변수를 `{key: value}` 형태로 기록하고 외부 렉시컬 환경 참조에 는 함수 밖의 변수와 함수를 포함하고 있습니다.

## 실행컨텍스트 생성과정
항상 전역객체를 담은 전역실행컨텍스트가 먼저 생성되고 함수가 있다면 함수의 실행컨텍스트 환경을 구성합니다. 
  
실행컨텍스트 내에는 렉시컬환경, 변수환경, this 바딩인 컴포넌트가 실행컨텍스트에 추가되고 환경레코드를 생성하여 렉시컬 환경 컴포넌트에 첨부합니다.  
외부 렉시컬 환경 참조를 생성하고 렉시컬 환경 컴포넌트에 첨부하고 숨김내부 프로퍼티 Scope 를 설정합니다.  
그다음 초기화를 진행하는데 호출한 함수의 파라미터 값을 함수 내부의 파라미터 이름에 매핑하고 환경 레코드에 작성합니다.  
만약 변수가 있다면 함수내부의 변수는 현재까지 undefined 입니다.  
그리고 실행단계로 오게되면 함수안의 코드를 실행하면서 변수에 값이 할당됩니다.

즉 호이스팅이라 불리는 개념은 실행컨텍스트가 생성되는 과정에서의 초기화과정에서 메모리에 식별자들이 등록되는 과정에서 발생하는것이고  
클로저는 실행컨텍스트의 렉시켤환경에 의해서 참조하고있는 외부 환경이 중첩된 함수 내부에 프로퍼티내에 존재하고 있기때문에 발생하는 현상이고   
스코프체인은 실행컨텍스트의 렉시컬환경에의해서 참조하고있는 변수들을 검색해 나가는 매커니즘입니다.


## 연습
```js
function book() {
    function get() {
        return point;
    };
    var point = 123;
    return get();
};
console.log(bool());
```
해당 예제는 인프런의 김영보님의 강의중 `자바스크립트 중고급: 근본 핵심 이해` 라는 강의에 나온 예제입니다.  
해당 예제를 실행컨텍스트관점에서 설명해보는 연습을 해보면 좋을것같습니다.
