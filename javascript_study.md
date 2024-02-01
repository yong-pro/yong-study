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
	
	