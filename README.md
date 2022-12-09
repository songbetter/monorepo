# yarn-berry-workspace

## [시작하기](https://github.com/songbetter/yarn-berry-workspace/commit/39bc196297ba8ddf42f265e4d98551c1dbeb2a8d)
yarn 버전을 변경하고 새로운 workspace를 생성하기.
```
yarn set version berry
yarn -w
```
![image](https://user-images.githubusercontent.com/75013112/206661215-9b9ff221-1257-44ac-9a74-f4e1877ca9df.png)

### [1. 워크스페이스에 apps 폴더 추가하기](https://github.com/songbetter/yarn-berry-workspace/commit/fb5a06b8148260a337447e75db2281da38dea501)
1. apps에 새로운 패키지 설치하기. 
```
yarn create next-app admin
```
![image](https://user-images.githubusercontent.com/75013112/206660470-83277803-9850-408d-b8d3-340d2d38915c.png)

2. root package.json 파일에서 workspaces 에 apps/* 추가하기
3. root에서 상태 갱신하기.
```
cd ..
yarn
```
![image](https://user-images.githubusercontent.com/75013112/206661272-54bda72c-6a98-4de5-84a1-d749c478440a.png)

## [2. pacakges/lib](https://github.com/songbetter/yarn-berry-workspace/commit/ec5eb1f7dab022ef74a3aff527341f40ba5654c3)

1. packages/lib 경로에서 yarn init 하여 package.json 생성하기
```
cd packages/lib
yarn init
```
2. package.json에 name, version, private, main, dependencies 부여하기
3. tsconfig.json 파일 생성하기
4. src 폴더에 index.ts 만들기 (hello from lib)
5. root에서 yarn 갱신하기
6. apps/admin에 @admin/lib 의존성 추가하기
```
yarn workspace admin add @admin/lib
yarn workspace admin run dev
```
![image](https://user-images.githubusercontent.com/75013112/206657751-1baec201-1f76-4c20-aa05-03b38cbc1912.png)

## 3. 공통 컨벤션 공유하기
### [3-1. tsconfig 설정 공유하기](https://github.com/songbetter/yarn-berry-workspace/commit/c20d9f77196cde56dca001f85afd963581e18707)
1. root 디렉토리에 tsconfig.base.json 파일 생성하기
2. apps, packages에서 설정한 teconfig.json 파일 수정하기
### [3-2. prettier, esling 설정 공유하기](https://github.com/songbetter/yarn-berry-workspace/commit/c20d9f77196cde56dca001f85afd963581e18707)
1. root에서 prettier, eslint 설치하기
```
yarn add prettier eslint eslint-config-prettier eslint-plugin-import eslint-plugin-react eslint-plugin-react-hooks eslint-import-resolver-typescript @typescript-eslint/eslint-plugin @typescript-eslint/parser -D
yarn dlx @yarnpkg/sdks
```
2. root에 .eslintrc.js 파일 추가하고 워크스페이스 별 생성된 기존 파일 삭제하기
3. .vscode/settings.json 설정 추가하기
```
  "eslint.packageManager": "yarn",
  "eslint.validate": ["javascript", "javascriptreact", "typescript", "typescriptreact"],
```
```
  "editor.defaultFormatter": "esbenp.prettier-vscode",
  "editor.formatOnSave": true,
  "editor.rulers": [120]
```

## [4. package/ui](https://github.com/songbetter/yarn-berry-workspace/commit/f16446d16a5e3a18d0f003d17345e713cd38ff56)
1. packages/ui 폴더 및 package.json 생성하기
2. package.json 파일을 열어서 name 변경하기
3. root에서 yarn 갱신하기
4. react dependency install
```
yarn workspace @admin/ui add typescript react react-dom @types/node @types/react @types/react-dom -D
```
5. packages/ui/tsconfig.json 설정하기
6. packages/ui/src 추가 index.ts, Button/tsx 파일 생성하기
7. packages/ui/package.json main 추가하기
8. apps/admin에 packages/ui 의존성 주입하기
```
yarn workspace admin add @admin/ui
```

## 5. typecheck
### [5-1. 각각의 프로젝트 typecheck하는 script 추가하기](https://github.com/songbetter/yarn-berry-workspace/commit/3d7f3c1be567a467d94b72298440c5c0e487d8ec)
```
"scripts": {
    "typecheck": "tsc --project ./tsconfig.json --noEmit"
  }
```
### [5-2. 모든 프로젝트를 typecheck하는 스크립트 추가하기](https://github.com/songbetter/yarn-berry-workspace/commit/0e42c6086c8765e359fa8f1d43beb63618a56c2a)
[workspace-tools 설치하기](https://yarnpkg.com/api/modules/plugin_workspace_tools.html)
```
yarn plugin import workspace-tools
```
```
 "scripts": {
    "g:typecheck": "yarn workspaces foreach -pv run typecheck"
 }
```
### typecheck 테스트
```
yarn workspace admin typecheck
```
## Peer Dependency
```
"peerDependencies":{
	"react" : "^16.8 || 18",
}
```
## Error
### [Typescript error](https://github.com/songbetter/yarn-berry-workspace/commit/ba19bf2004ee240c15639faad074c10168bd010a)
![image](https://user-images.githubusercontent.com/75013112/206661116-69409e1e-cdbc-4484-9db7-c4baceddb1ea.png)

```
yarn add -D typescript
yarn dlx @yarnpkg/sdks vscode
```

### Typescript Compile Error
1. typescript 파일을 javascript로 변환하기
```
yarn workspace admin add next-transpile-modules
```
2. apps/admin/next.config.js 파일 수정하기
```
// @admin/ui 패키지를 tranpile 시킨다.
const withTM = require('next-transpile-modules')(['@admin/ui']);

/** @type {import('next').NextConfig} */
const nextConfig = {
  reactStrictMode: true,
  swcMinify: true,
};

module.exports = withTM(nextConfig);
```

## Reference
[yarn init](https://yarnpkg.com/cli/init)<br/>
[yarn workspaces foreach](https://yarnpkg.com/cli/workspaces/foreach)
