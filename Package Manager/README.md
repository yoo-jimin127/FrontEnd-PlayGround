# Package Manager

## ✅ 패키지 매니저란?
- **패키지 매니저**(Package manager) : 패키지를 다루는 작업을 편리하고 안전하게 수행하고자 사용되는 툴 
    - 패키지를 다루는 작업 : 설치, 업데이트, 수정, 삭제 etc.
- **패키지**(Package) : 코드의 배포를 위해 사용되는 코드의 묶음 (라이브러리 : 코드의 묶음)
    - 라이브러리 & 실행 파일 포함

**패키지 매니저 Top 3**      
- [npm](https://docs.npmjs.com/)
- [Yarn(Yarn Classic)](https://yarnpkg.com/) → v2 이상의 [Yarn Berry](https://yarnpkg.com/)
- [pnpm(고성능 npm)](https://pnpm.io/)

## ✅ 패키지 매니저 역할
npm, Yarn, pnpm 모두 역할은 대부분 동일하다.   
- 패키지의 dependency 관리(일괄(Batch) 설치 or 업데이트)
- 패키지 신뢰성 & 손상되지 않음을 보장 (보안 감사(audit) 수행)
- 기능에 따른 여러 패키지의 그룹화
- 패키지 압축 해제
- SW repository로부터 패키지 검색, 다운로드, 설치, 업데이트 수행
- 메타데이터 처리 및 쓰기
- 스크립트 실행
- 패키지 배포(publish)

따라서 설치 속도, 스토리지 사용량, 기존 워크플로우와 결합되는 방식 등을 고려해 패키지 매니저를 결정한다.   

## ✅ 패키지 매니저 종류
|**Language**|**Package Manager**|**Software Repository**|
|:---:|---|---|
|Python|pip|PyPI|
|PHP|Composer|Packagist|
|Node.js|npm, Yarn, pnpm|npm, Yarn, pnpm|
|Java|Maven, Gradle|Maven|
|Ruby|RubyGems, Bundler|RubyGems, Bundler|

## ✅ Node.js 환경의 패키지 매니저 분석
node.js 환경의 패키지 매니저로 크게 npm과 yarn, pnpm이 존재하며,  
패키지 매니저의 기능은 동일하나 내부적인 차이점이 존재한다.   
- `npm`, `Yarn` : `node_modules` 폴더에 dependency 설치
- `pnpm` : 중첩된 `node_modlues` 폴더에 dependency를 저장하는 방식을 개선하기 위한 개념 도입
- `Yarn-berry` : `PnP`(Plug'n'Play) 모드 (`node_modules` X)

|**Link**|
|:---|
[📚 npm 특징 정리 & 분석]()|
[📚 Yarn classic 특징 정리 & 분석]()|
[📚 pnpm 특징 정리 & 분석]()|
[📚 Yarn Berry 특징 정리 & 분석]()|

## 📌 참고 자료
- [package와 package manager 분석](https://velog.io/@gil0127/Package-%EC%99%80-Package-manager)
- [패키지 매니저(Package Maganer)란?](https://computer-science-student.tistory.com/402)
- [[번역] JavaScript 패키지 매니저 비교 - npm, Yarn 또는 pnpm?](https://dev-boku.tistory.com/entry/%EB%B2%88%EC%97%AD-JavaScript-%ED%8C%A8%ED%82%A4%EC%A7%80-%EB%A7%A4%EB%8B%88%EC%A0%80-%EB%B9%84%EA%B5%90-npm-Yarn-%EB%98%90%EB%8A%94-pnpm)