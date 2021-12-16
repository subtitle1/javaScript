# 자바스크립트의 함수
- 자바스크립트의 함수를 정의하는 세가지 방법
```javascript
  // 함수선언
  function fn1() {
    console.log('fn1 함수');
  }
  
  // 익명함수
  var fn2 = function() {
    console.log('fn2 함수');
  }
  
  // 화살표 함수
  var 변수명 = () => 수행문;
```
![image](https://user-images.githubusercontent.com/87356533/146354096-3137aa78-e1f0-4b47-bab0-ae1e111e7b8e.png)

- 자바스크립트에서는 함수를 매개변수로 전해줄 수 있다.
```javascript
  function calc(num1, num2, fn) {
    fn(num1, num2);
  }
  
  function plus(a, b) {
    console.log(a+b);
  }
  
  // 첫번째 방법
  clac(10, 20, plus);
  
  // 두번째 방법, 함수 안에서 함수를 즉석으로 구현할 수도 있다
  calc(10, 20, function(a, b) {
    console.log(a+b);
  });
  
  // 세번째 방법
  calc(10, 20, (a, b) => a - b);
  calc(10, 20, (a, b) => {return a - b}); // 중괄호가 있으면 반드시 return이 있어야 한다
```
