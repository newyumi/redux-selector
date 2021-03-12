> 강의 버전에서 packages 업데이트함 
> current node v14.16.0
> yarn upgrade --latest
> remove babel-jest
> Using firebase for login, cloud firestore authorization will be expired.

<br/>

## study 125 - 132
---

### 125: find()
만족하는 첫 번째 요소의 값을 반환 없으면 undefined
```javascript 
const array1 = [5, 12, 8, 130, 44];
const found = array1.find(element => element > 10);

console.log(found); // expected output: 12
```

<br/>

### 126: cart item component
cart-dropdown component에서 사용 
Add to cart 버튼 (addItem)을 누르면 addItem action 실행

<br/>

### 127: reduce()
```javascript
const array1 = [1, 2, 3, 4];
const reducer = (accumulator, currentValue) => accumulator + currentValue;

// 1 + 2 + 3 + 4
console.log(array1.reduce(reducer));
// expected output: 10

// 5 + 1 + 2 + 3 + 4
console.log(array1.reduce(reducer, 5));
// expected output: 15

param 4종류: accumulator(누적값), current value, index, src (원본 배열)
```

<br/>

### 128: selectors in Redux
```javascript
const mapStateToProps = ({ cart; { cartItems } }) => ({
	itemCount: cartItems.reduce(
		(accumalatedQuantity, cartItem) => accumalatedQuantity + cartItem.quantity,
		0
	)
})
```

컴포넌트에서 props로 store의 값을 가져올 때, 만들었던 selector를 통해 가져오면 state에서 필요한 값만 가져오거나 원하는 형태로 계산해서 가져올 수 있음. 

컴포넌트마다 다른 형태로 값을 가져오더라도 selector만 관리하면 되기 때문에 store를 깨끗하게 관리

But, selector를 사용하면 state가 변경될 때마다 selector 함수가 실행. 
state 변경마다 계산을 수행하면 성능 상의 이슈가 발생 확률 높아짐.

-> reselect로 해결, 이전값이랑 같으면 저장된 값을 반환 
캐싱을 통해 동일한 계산 방지, 성능 향상

<br/>

### 130: reselect library
`import { createSelector } from 'reselect'`

 cart.selector.js 파일 참조

<br/>

### 132. user selectors

- Selectors can compute derived data, allowing Redux to store the minimal possible state.
- Selectors are efficient. A selector is not recomputed unless one of its arguments changes.
- Selectors are composable. They can be used as input to other selectors.

<br/>

### 정리 
`상태`는 읽기 전용!

`store에 저장하는 acton을 setter, selector를 getter에 비유`

`리듀서` 함수에서는 액션의 타입에 따라 변화된 상태를 정의하여 반환
이전 상태와 액션 객체를 파람으로 받음
이전의 상태는 건들이지 않고, 변화를 일으킨 새로운 상태 객체를 만들어서 반환

`selector`는 store에 저장된 state에서 필요한 데이터를 선별적으로 가져오거나, 계산을 수행해서 원하는 형태의 데이터를 가져온다

`mapStateToProps`는 스토어가 가진 state를 어떻게 prop에 엮을지 정의
`mapDispatchToProps`는 reducer에 action을 알리는 함수 dispatch를 어떻게 props에 엮을지 정의 
action을 dispatch 함수에 넘겨줌으로써 실행 -> 모든 reducer가 실행
reducer는 관계없는 action은 무시하고 주어진 action만을 처리하도록 설정해야한다

[참고 링크](https://medium.com/@ca3rot/%EC%95%84%EB%A7%88-%EC%9D%B4%EA%B2%8C-%EC%A0%9C%EC%9D%BC-%EC%9D%B4%ED%95%B4%ED%95%98%EA%B8%B0-%EC%89%AC%EC%9A%B8%EA%B1%B8%EC%9A%94-react-redux-%ED%94%8C%EB%A1%9C%EC%9A%B0%EC%9D%98-%EC%9D%B4%ED%95%B4-1585e911a0a6)