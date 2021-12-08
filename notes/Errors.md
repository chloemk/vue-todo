# 에러노트

`No inputs were found in config file Specified 'include' paths were '["**/*"]' and 'exclude' paths were '[]'.`
tsconfig.json과 같은 레벨에 ts 파일이 없어서 나는 에러다. ts파일을 만들고 editor를 껐다 키면 에러 해결된다.
TypeScript does not resolve webpack aliases automatically

투두를 입력했을 때 바로 목록에 반영이 안되는 문제점이 생겼다.

## 프로젝트 구조

Babel, TS, Linter

## 노트

computed는 반환 타입을 정의해줘야한다. 그래야지 반환타입에 대해서 다른 것들도 추론을 정확하게 받을 수 있다.
preset -> vue 플러그인 집합
"build": "vue-tsc --noEmit && vite build" // build task에 vue-stc --noEmit을 해야지 타입체크를 해준다.
typescript and vue-tsc for types checking using a command line. You may skip these dependencies if you rely on types checking in your IDE (Vue doesn't use typescript to build the project).
https://moiva.io/blog/the-missing-migration-guide-from-vue-cli-to-vite/

vue-add typescript // -> 비추. 점진적으로
