# javascript 

### backtag ` ${} 보간법

```javascript
	console.log(" 이름 ${ff} "); // 더블
	console.log(' 이름 ${ff} '); // 싱글
	console.log(` 이름 ${ff} `); // 백텍 만작동

```

### "use strict"; 엄근모드


### 원시타입 아래말고는 타입구분됨
	* null -> object
	* array -> object
	* 함수 -> function
	
### 변수선언
	var --> function scope 
	let --> block scope 더쫍음
	const --> 상수 선언 값할당 변경 불가 객체선언하지말것
	
### 일치 연산 ===
	NaN === NaN // false, Number.isNan() 함수로 비교해야함
	0 === -0 // true, Object.is() 함수로 비교
	
### 객체의 비교는 독자성일치를 비교한다.
```javascript
	var x = [1, 2, 3];
	
	var y = x;
	
	y === x // true
	y === [1, 2, 3] //false
	x === [1, 2, 3] //false
```

### 동등비교 연산자 == 
	두값의 비교전에 같은 변수타입으로 강제변환후 비교하게됨   
	<=, >=, <, > 도 강제변환후 비교함
	42 == "42" // true
	1 == true // true
	
### clouser 
	함수가 선언될 때(실행X) 외부의 lexcial environment를 참조하게 되는 현상이다.
	클로저는 내부에 선언된 함수가 외부함수의 지역변수를 사용해 줬을 때만 클로저라고 선언된다.
	
### this 키워드
	전역에서의 this는 기본적으로 window 객체입니다. strict mode에서는 undefined입니다.
	일반 함수 또는 내부함수의 this는 전역 객체를 참조한다.
	객체 메서드 또는 프로토타입 메서드에서 this는 해당 메서드를 호출한 객체를 참조한다.
	생성자 함수 내부의 this는 생성된 객체를 참조한다.
	DOM event handler로 사용되는 함수 내부의 this는 이벤트가 발생한 element로 설정된다. 
	외부참조를 위해서는 call, bind 에 this파라메터로 외부 this참조할수있다.