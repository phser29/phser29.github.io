---
layout: single
title: "react-basket"
categories: javaScript
tag: react
toc: true
---

# (JSON) 쇼핑몰 장바구니

## JSON 상품 출력

- axios를 활용하여 json 데이터 조회
- find 함수로 id 값과 일치하는 데이터 출력 

```
// 훅으로 상품 지속적으로 출력
useEffect(() => {
  axios.get("/data/products.json").then(data => {
    setProduct(data.data.products.find((product) => product.id === parseInt(id)))
  })
}, [id]);
```

## 장바구니 추가

- JS 객체를 생성하여 장바구니 클릭 시 해당 정보가 장바구니로 넘어가서 배열에 저장

```
const handleCart = () => {
  const cartItem = {
    id: product.id,
    image: product.image,
    name: product.name,
    price: product.price,
    provider: product.provider,
    quantity: count
  }
  // 장바구니 cartItem와 일치하는 cart.id가 있으면 카운트 증가 및 상품 담기
  const found = cart.find((el) => el.id === cartItem.id);
  if(found) {
    setQuantity(cartItem.id, found.quantity + count);
  } else {
    setCart([...cart, cartItem]);
  }
}
```

## 장바구니 중복 제한

- 배열로 넘어간 데이터와 일치하는 id가 있으면 다음 공간으로 저장

```
const setQuantity = (id, quantity) => {
  const found = cart.filter((el) => el.id === id)[0];
  const idx = cart.indexOf(found);
  const cartItem = {
    id: product.id,
    image: product.image,
    name: product.name,
    price: product.price,
    provider: product.provider,
    quantity: quantity,
  };
  //js 배열은 ...배열 전후로 값 추가가능
  setCart([...cart.slice(0, idx), cartItem, ...cart.slice(idx + 1)])
}
```
*필터는 배열을 반환*

- 리액트 체크박스 리스트

```
const handleCheckList = (checked, id) => {
  if(checked) {
    setCheckLists([...checkLists, id]);
  } else {
    setCheckLists(checkLists.map((check) => check !== id));
  }
}
```

- 리엑트 체크박스 전체 선택 함수
- state로 선택 함수 적용

```
const handleAllCheck = (checked) => {
  if(checked) {
    const cartItems = [];
    cart.map((cart) => cartItems.push(cart.id))
    setCheckLists(cartItems);
  } else {
    setCheckLists([]);
  }
}
```