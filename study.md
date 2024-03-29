# 자바스크립트 이론 정리

## 배열

- 배열의 마지막 요소 인덱스 => 배열.length - 1
- 원했던 배열의 제일 앞에 값을 추가하는 방법 => unshift 사용
  - ex) 배열.unshift();
- 원했던 배열의 제일 뒤에 값을 추가하는 방법 => push 사용 or 배열[배열.length] = 값
- 배열에서 마지막 요소 제거하는 방법 => pop 사용
- 배열에서 첫 번째 요소 제거하는 방법 => shift 사용
- 중간 요소 제거 방법 => splice 사용
  - splice(지우려는 인덱스 시작 번호, 지우려는 개수)
  - 지우려는 개수 미작성 시, 시작 번호부터 끝까지 모든 요소를 제거하겠다는 뜻임
    - splice는 제거 뿐만 아니라 다른 값도 넣을 수 있음(세 번째 자리부터 바꿀 값들을 넣어주면 됨)
- 배열에서 특정 요소가 있는지 찾는 방법 => includes 사용(true/false로 알려줌)
- 배열에서 특정 요소가 몇 번째 인덱스에 위치하는지 찾는 방법 => indexOf or lastIndexOf (없으면 -1 출력)

### const인데 수정이 가능한 이유?

    새로운 값을 대입(=)하지 못한다고 기억하면 됨 -> 객체 내부의 속성이나 배열의 요소는 수정할 수 있음!

## 메서드(method)

- 객체 안에 들어있는 함수

## 객체 간의 비교

```javascript
{} === {} // false
```

- 객체 간 비교 시 false가 나옴
- 같은 객체인지 비교하고 싶으면 변수에 저장해서 비교해야함

## 선택자

- document.querySelector('input'); 인풋인 태그 선택
  - 인풋인 태그가 여러 개인 경우 제일 첫 번째 인풋 선택
- document.querySelectorAll('input'); 인풋인 태그 모두 선택

- \#은 아이디 (고유 값일 때 주로 사용)
- \.은 클래스 (여러 개일 때 주로 사용)
- div span과 같이 공백인 경우 자식과 자손 선택 가능
- div>span과 같이 >인 경우 바로 밑에 자식만 선택 가능
- 너무 복잡하다 생각할 시 id 부여해주면 편함

## 콜백 함수(=리스너 함수)

    어떤 동작을 실행하고 난 뒤 연이어 실행되는 함수

- 이벤트를 만들 때 사용하는 메서드 : addEventListener

## 고차 함수(high order function)

    함수를 리턴하는 함수 => 함수 간의 중복을 제거하기 위하여 사용

```javascript
const a = (number) => () => {
  console.log(number);
}; // return 생략 버전

/* 둘 다 같은 함수임 */

const a = (number) => {
  return () => {
    console.log(number);
  };
}; // return 생락X 버전
```

## 기존 코드 중첩 제거 방법

1. if문 다음에 나오는 공통된 절차를 각 분기점 내부에 넣음
2. 분기점에서 짧은 절차부터 실행하게 if문 작성
3. 짧은 절차가 끝나면 return(함수 내부의 경우)이나 break(for문 내부의 경우)로 중단
4. else를 제거(이 때 중첩 하나가 제거됨)
5. 다음 중첩된 분기점이 나오면 1~4의 과정을 반복

## event.preventDefault()

    기본 동작 막기
    => form은 버튼 클릭 시 새로고침 됨(이 동작을 막기 위해 사용)

## Set

    - 중복을 제거해줌
    - 생성자 함수로 생성(new Set())
    - 개수를 알고 싶을 때는 .size 사용

## join 메서드

    배열을 문자열로 바꿔주는 메서드
    (',')이 기본값

## split 메서드

    문자열을 배열로 바꿔주는 메서드

## document.createElement, document.createTextNode

    각각 태그, 텍스트를 만드는 메서드
    but, 다른 태그에 append나 appendChild 하기 전까지는 화면에 보이지 않음

## appendChild, append

    document.createElement, document.createTextNode로 만든 태그나 텍스트를 선택한 태그의 자식 태그로 넣음
    appendChild는 하나만 넣을 수 있고, append는 여러 개를 동시에 넣을 수 있음
    append 사용 시 document.createTextNode 대신 문자열을 바로 넣어도 됨

## forEach 메서드

    .forEach((element, index) => {})
    배열 각 자리마다 함수를 적용해주는 메서드(반복문 역할)

```javascript
const answer = [3, 1, 4, 6];
const value = "3214";
let strike = 0;
let ball = 0;
for (let i = 0; i < answer.length; i++) {
  const index = value.indexOf(answer[i]);
  if (index > -1) {
    if (index === i) {
      strike += 1;
    } else {
      ball += 1;
    }
  }
}

/* 위와 아래의 코드는 동일하게 작동 */

const answer = [3, 1, 4, 6];
const value = "3214";
let strike = 0;
let ball = 0;
answer.forEach((element, i) => {
  const index = value.indexOf(element);
  if (index > -1) {
    if (index === i) {
      strike += 1;
    } else {
      ball += 1;
    }
  }
});
```

## map 메서드

    .map((element, index) => {})
    배열의 요소를 순회하면서 값을 바꿔주는 메서드
    forEach의 역할을 하면서 값도 바꿔줌
    but, 기존의 배열은 바뀌지 않고 return 값대로 새로운 배열을 생성함

```javascript
const array = [1, 2, 3, 4];
array.map((element, i) => {
  return element * 2;
});
```

## fill 메서드

    원하는 값으로 빈 배열을 채워줄 수 있음

```javascript
Array(9).fill();
// 크기가 9인 빈 배열을 생성 후 undefined로 채움

Array(9).fill(0);
// 크기가 9인 빈 배열을 생성 후 0으로 채움

/* map과 혼합해서 사용하는 방법 -----------------------
  for문을 사용하지 않고도 차례대로 배열을 채울 수 있음! */

Array(9)
  .fill(0)
  .map((element, index) => {
    return index + 1;
  });
// [1, 2, 3, 4, 5, 6, 7, 8, 9]
```

## slice 메서드

    .slice(start, end) => start부터 end전까지 자르는 메서드
    원본을 변화시키지도 않고, 추가 불가능

## sort 메서드

    .sort((a, b) => a - b); // 오름차순
    .sort((a, b) => b - a); // 내림차순
    원본을 변화시키기 때문에, slice로 복사하고 sort하는 방식을 추천
    문자열 비교하려면 a[0].charCodeAt() - b[0].charCodeAt()해서 앞글자 비교하거나 a.localCompare(b)쓰면 완벽 오름차순(사전순) 정렬 가능

### var과 let의 차이

    var는 '함수' 스코프를 가지고, let은 '블록' 스코프를 가짐

### .과 []의 차이

```javascript
let computerChoice = "scissros";
const rspX = {
  scissors: "0",
  rock: "-220px",
  paper: "-440px",
};
/* rspX.computerChoice 하면 문자열 속성,
   rspX[computerChoice] 하면 값(rspX['scissors'])이 전달 */
```

#### \*\*\* setInterval은 재귀 setTimeout으로 바꿔쓸 수 있음 but, 같은 것은 아님

#### \*\*\* 객체에 참조 관계를 유지하고 싶으면 변수에 저장하여 변수를 재사용해야함

### || 줄이는 꿀팁

```javascript
if (
  diff === "고양이" ||
  diff === "강아지" ||
  diff === "사자" ||
  diff === "거북이"
)
  /* 위의 ||를 사용한 코드를 밑의 배열과 includes 메서드를 통하여 줄일 수 있음 */
  ["고양이", "강아지", "사자", "거북이"].includes(diff);
```

## add, replace, remove 메서드

    태그.classList.add('클래스'); // 추가
    태그.classList.replace('기존클래스', '수정클래스'); // 교체
    태그.classList.remove('클래스'); // 제거

## reduce 메서드

    배열.reduce((누적값, 현재값) => {
      return 새로운 누적값;
    }, 초기값);
    // 초기값 제공하지 않을 경우 배열의 첫 번째 요소가 초기값이 됨

### parentNode/children

    parentNode : 현재 태그의 부모 태그를 찾음
    children : 현재 태그의 자식 태그를 찾음

## flat 메서드

    2차원 배열을 1차원 배열로 만들어줌(3차원이면 2차원으로)

## every/some 메서드

    every => 모든 조건이 true여야 true(하나라도 false면 중단)
    some => 하나의 조건이라도 true면 true, 반복 중단

## 이벤트 버블링

    이벤트가 발생할 때 부모 태그에도 동일한 이벤트가 발생하는 현상
    - *주의* 이벤트 버블링 현상 발생 시 이벤트 리스너 콜백 함수의 event.target은 이벤트가 발생한 태그로 바뀜
      - 이벤트가 발생한 태그가 아닌 이벤트를 연결한 태그에 접근 원할 경우 event.currentTarget 사용

## 깊은 복사와 얕은 복사

    const monster = JSON.parse(JSON.stringify(monsterList[0]));
    // 깊은 복사
    const monster = { ...monster[0] } // 객체 리터럴 얕은 복사
    const arr = [...arr]; // 배열 얕은 복사(slice나 concat 메서드도 가능)
    얕은 복사 = 가장 바깥 객체만 복사되고 내부 객체는 참조됨
    깊은 복사 = 내부의 참조를 끊어내고 싶을 때 사용
    객체 안에 객체가 들어있지 않는 한 얕은 복사 하면됨

## this

    화살표 함수가 아닌 function 일 때 this가 제대로 작동
      ** 객체.메서드를 해야 그 객체가 this가 됨
    화살표 함수일 경우 this는 window가 됨
    this는 함수가 호출될 때 결정됨
    bind 메서드 사용해서 직접 바꿀 수 있음

## 클래스

    객체를 생성하기 윈한 템플릿(서식)

## concat 메서드

    배열을 하나 풀어서 합친다.
    [1].concat(2) === [1].concat([2]) => 둘 다 [1, 2]로 나옴

## 호출 스택과 이벤트 루프 개념

    호출 스택 : 함수가 실행되는 공간
    백그라운드 : 타이머를 처리하고 이벤트 리스너를 저장하는 공간
    테스크 큐 : 타이머나 이벤트 리스너의 콜백 함수가 들어있는 공간(대기하는 공간/함수를 직접 실행하지는 않음)
    이벤트 루프 : 호출 스택이 비어있을 때, 테스트 큐에 있는 함수를 하나씩 꺼내서 실행해주는 역할

## &&, ||, optional chaining, nullish coalescing

    A && B : A가 존재하는 경우 B를 실행
    A || B : A가 존재하지 않는 경우 B를 실행
      -> 0, 빈 문자열, false, null, undefined, NaN
    ?. : 존재하면 실행하라는 의미(보호 연산자)
      -> 앞에 있는 것이 참인 값이면 뒤 코드 실행, 거짓인 값이면 코드를 통째로 undefined 만들어버림
      -> 객체는 .을 사용하기에 상관 없지만 배열은 무조건 ?. 세트로 써야하는 점 잊지 말기!(함수에서도 사용 가능)
    A ?? B : null이나 undefined가 아니면 A, 맞으면 B 실행

## 재귀 시 Maximum call stack size exceeded(최대 호출 스택 사이즈 초과) 해결 방법

    호출 스택만 과부하가 걸리고 백그라운드와 테스트 큐는 비어있음
    코드를 백그라운드와 테스트 큐에 보내는 가장 간단한 방법은 setTimeout(와 같은 비동기 함수) 사용
      -> 재귀 함수 사용 시 연산량이 많으면 브라우저가 느려지는 현상 발생. 연산량을 최소화 할 수 있게 코드 작성 요망

## 마우스 우클릭 이벤트

    contextmenu
      기본적으로 브라우저 메뉴를 띄우므로 기본 동작 막으려면 event.preventDefault 메서드 호출

### 변수는 반드시 선언 이후에 사용해야 되지만, 함수는 순서에 상관이 없음(function 키워드 일 때만)

## clientX, clientY / pageX, pageY

    clientX는 현재 브라우저 페이지 내에서의 x 좌표를 가리킴
    pageX도 브라우저 페이지 내에서의 x 좌표를 가리키지만, 스크롤이 있는 경우 스크롤한 픽셀 값까지 포함

## offsetX, offsetY / screenX, screenY

    offsetX는 이벤트를 연결한 대상을 기준으로 마우스의 x 좌표를 가져옴
    페이지 내의 다른 태그에 마우스 이벤트를 걸면 해당 태그의 왼쪽 모서리 좌표가 0이 됨
    screenX는 모니터를 기준으로 잡아 모니터의 왼쪽 모서리가 0이 됨

## mouseeventX, mouseeventY / mousemove / mousedown, mouseup

    mouseevent는 얼마나 마우스를 움직였는지 표시
    mousemove 이벤트 경우에만 실제 값이 잡힘
    mousedown, mouseup는 마우스 방향을 판단할 때 사용

## documentFragment

    실무에서 화면에 태그 추가 시 createElement로 만들어서 실제 태그에 바로 추가하는 방식을 잘 사용하지 않음. 대신 document.createDocumentFragment 메서드로 메모리 안에서만 존재하는 documentFragment를 만들고, documentFragment안에 필요한 태그를 추가한 뒤 마지막으로 한 번에 추가하는 방식을 사용함

## 키보드 이벤트

    대표적인 키보드 이벤트 => keydown, keyup (키보드를 누를 때와 눌렀다 뗄 때 각각 호출)
    어떤 키를 눌렀는지는 event.key 속성에 나옴
    왼쪽은 ArrowLeft, 오른쪽은 ArrowRight, 위쪽은 ArrowUp, 아래쪽은 ArrowDown
    속성 기능도 제공하여 다른 키와 동시에 누르는 것도 알아낼 수 있음

## 마우스 이벤트

    대표적인 마우스 이벤트 => mousedown, mouseup, mousemove (마우스를 클릭할 때, 클릭했다가 뗄 때, 마우스를 이동할 때 각각 호출)
    이벤트 속성에서 x, y 좌표 얻을 수 있으며 이를 이용해 마우스 위치 변화를 잡아낼 수 있음
