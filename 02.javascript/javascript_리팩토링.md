1. map 변환

```javascript

const naverLogin = (id) => { return '네이버'; };
const kakaoLogin = (id) => { return '카카오'; };
const facebookLogin = (id) => { return '페이스북'; };
const googleLogin = (id) => { return '구글'; };

const executeLoginMap = {
    naver: naverLogin,
    kakao: kakaoLogin,
    facebook: facebookLogin,
    google: googleLogin,
};

const socialLogin = (where, id) => {
    let domain = executeLoginMap[where](id); // naver일 경우 naverLogin(id) 로 함수 실행
    return `${domain} ${id}`;
};
```


2 책임연쇠방법

```javascript

const Handler = {
    result: '',
    count: 0,
    rules: [
        {
            // match는 false일 경우 다음 match로 넘어가게 된다.
            match(isLogin, checkToken, user) {
                return isLogin ? true : false; // 1. 로그인 여부 확인
            },
            // action은 match가 true 인 실행 부분을 기재한다
            action(isLogin, checkToken, user) {
                Handler.result = '이미 로그인 중';
                Handler.result += ` (+ 시도 횟수 ${Handler.count++}번)`;
                return Handler.result;
            },
        },
        {
            match(isLogin, checkToken, user) {
                return !checkToken ? true : false;  // 2. 토큰 존재 확인
            },
            action(isLogin, checkToken, user) {
                throw new Error('에러 - 토큰이 없습니다 !');
            },
        },
        {
            match(isLogin, checkToken, user) {
                return user.nickName == undefined ? true : false; // 3. 가입 여부 재확인
            },
            action(isLogin, checkToken, user) {
                registerUser(user); // 회원 가입하기
                Handler.result = '회원가입 성공';
                Handler.result += ` (+ 시도 횟수 ${++Handler.count}번)`;
                return Handler.result;
            },
        },
        {
            match(isLogin, checkToken, user) {
                return true; // 마지막 핸들러 부분이니까 바로 action() 이 실행되도록
            },
            action(isLogin, checkToken, user) {
                refreshToken(); // 토큰 발급
                Handler.result = '로그인 성공';
                Handler.result += ` (+ 시도 횟수 ${++Handler.count}번)`;
                return Handler.result;
            },
        },
    ],
};


//호출결과
const socialLogin = (isLogin, checkToken, user) => {
    let result = '';

    // {march, action} 핸들러 객체가 들어있는 의사 결정 규칙 배열 rules를 순회하면서
    for (const rule of Handler.rules) {
        // 만일 해당 분기에 해당되면
        if (rule.match(isLogin, checkToken, user)) {
            result += rule.action(isLogin, checkToken, user); // 그 분기의 실행부를 호출한다
            return result;
        }
    }
};

console.log(loginService(false, true, { nickName: 'inpa' })); // 로그인 성공 (+ 시도 횟수 1번)
console.log(loginService(true, false, { nickName: 'inpa' })); // 이미 로그인 중 (+ 시도 횟수 1번)
console.log(loginService(false, true, {})); // 회원가입 성공 (+ 시도 횟수 1번)
console.log(loginService(false, false, { nickName: 'inpa' })); // Error: 에러 - 토큰이 없습니다 !
출처: https://inpa.tistory.com/entry/⚙️-if-else-refactoring [Inpa Dev 👨‍💻:티스토리]

```


