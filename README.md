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

##[3. ]()
## Error
### [Typescript error](https://github.com/songbetter/yarn-berry-workspace/commit/ba19bf2004ee240c15639faad074c10168bd010a)
![image](https://user-images.githubusercontent.com/75013112/206661116-69409e1e-cdbc-4484-9db7-c4baceddb1ea.png)

```
yarn add -D typescript
yarn dlx @yarnpkg/sdks vscode
```
## Reference
[yarn init](https://yarnpkg.com/cli/init)<br/>
