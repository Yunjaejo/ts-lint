# eslint, typescript

<hr>

# eslint 설정하기
### (Webstorm, typescript 기준입니다.)

typescript, eslint devDependencies 추가

```shell
$ npm init -y  # package.json
$ tsc --init  # tsconfig.json
$ npm i -D eslint
$ npm i -D eslint eslint-config-airbnb-base eslint-plugin-import
$ npm i -D @typescript-eslint/eslint-plugin @typescript-eslint/parser
```

eslint-config-prettier? Prettier와 충돌할 설정들을 비활성화 <br>
eslint-plugin-prettier? 코드 포맷할 때 Prettier를 사용하게 만드는 규칙 추가 <br>

필요할 때 다운받도록 하자.

프로젝트 최상위에 .eslintrc.js 파일을 만들고 이를 추가해준다.
```js
// .eslintrc.js
module.exports = {
  parser: '@typescript-eslint/parser',
  plugins: ['@typescript-eslint'],
  extends: [
    // Airbnb style guide 적용
    'airbnb-base',
    // TypeScript ESLint recommanded style 적용
    'plugin:@typescript-eslint/eslint-recommended',
  ],
  rules: {
    'no-console': process.env.NODE_ENV === 'production' ? 'error' : 'off',
  },
};

```

package.json 에서 scripts 추가
```js
{
  "scripts": {
    // linting scripts
    "lint": "eslint src/**/*.ts",
    "lint:fix": "eslint --fix src/**/*.ts"
  },
```

lint 실행하기
```shell
$ npm run lint # eslint실행, 오류를 발견해줌
$ npm run lint:fix # eslint --fix실행, 오류를 리포맷해줌
```

<hr>

기본적으로 웹스톰에는 eslint, prettier가 내장되어있어 옵션을 켜주면 빨간줄로 에러를 감지해준다.

즉 lint는 패시브니까 lint:fix로 한번에 모든것을 잡자.

VSCODE에서는 eslint 익스텐션을 깔아서 에러를 시각화할 수 있다.
