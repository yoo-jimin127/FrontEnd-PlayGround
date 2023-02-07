# Yarn Berry
`node_modules` 없이 `node`를 사용할 수 있는 환경인 `yarn berry`를 알아보자.   
- 사전 지식 정리 공간: [패키지 매니저란 무엇인가?](https://github.com/yoo-jimin127/FrontEnd-PlayGround/blob/main/Package%20Manager/README.md)

## 1️⃣ 서론 1 - 패키지 매니저의 역할
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

## 1️⃣ 서론 2 - 패키지 매니저 종류
|**Language**|**Package Manager**|**Software Repository**|
|:---:|---|---|
|Python|pip|PyPI|
|PHP|Composer|Packagist|
|Node.js|npm, Yarn, pnpm|npm, Yarn, pnpm|
|Java|Maven, Gradle|Maven|
|Ruby|RubyGems, Bundler|RubyGems, Bundler|

## 1️⃣ 서론 3 - Node.js 환경의 패키지 매니저 분석
node.js 환경의 패키지 매니저로 크게 npm과 yarn, pnpm이 존재하며,  
패키지 매니저의 기능은 동일하나 내부적인 차이점이 존재한다.   
- `npm`, `Yarn` : `node_modules` 폴더에 dependency 설치
- `pnpm` : 중첩된 `node_modlues` 폴더에 dependency를 저장하는 방식을 개선하기 위한 개념 도입
- `Yarn-berry` : `PnP`(Plug'n'Play) 모드 (`node_modules` X)

## 2️⃣ 본론 1 - Yarn Berry
`Yarn Berry`는 `Node.js`를 위한 새로운 패키지 관리 시스템이다.   
`Yarn v1`(`Yarn classic`)에서 2020.01.25 정식 버전 `Yarn v2`(`Yarn Berry`)가 출시되었으며,   
현재 `Yarn Berry`는 `Babel`을 비롯한 큰 오픈소스 레포지토리에서도 채택되어 사용 중에 있다.   
- [Yarn Berry Github](https://github.com/yarnpkg/berry) 

## 2️⃣ 본론 2 - 왜 Yarn Berry인가?(1) (Feat. NPM의 문제점)
<img src="https://user-images.githubusercontent.com/66112716/217190042-7470dcac-e1ce-4c51-bbbe-0b00484705f5.png" width="600" />

위와 같이 `NPM`은 `Node.js`를 설치할 경우 기본적으로 제공되는 패키지 매니저이지만 비효율적이거나, 깨져 있는 부분이 많다.   

### ▶️ NPM의 문제점
1. **패키지가 중복으로 설치될 수 있다는 단점 존재**
<br>

2. **의존성 검색의 비효율성**
    - 느린 I/O 호출의 반복 → 경우에 따라 I/O 호출의 실패로 이어진다.
<br>

3. **환경에 따라 달라지는 동작**
    - 상위 디렉토리 환경에 따라 의존성 호출의 변수 발생
<br>

4. **비효율적인 설치**
    - 매우 큰 `node_modules`의 공간 차지
    - `node_modules`디렉토리 구조 구축을 위한 큰 비용의 I/O 작업
<br>

5. **유령 의존성**
    - 중복되어 설치되는 `node_modules`를 아끼기 위해 호이스팅 기법 사용 (NPM, Yarn v1)<br>
    <img src="https://user-images.githubusercontent.com/66112716/217192789-1363b48a-e6c8-402c-9ef4-a4c156adbc77.png" width="600" /><br>
    - 위와 같은 의존성 트리가 구축되어 있다면, [A (1.0)]과 [B (1.0)] 패키지의 중복 설치로 디스크 공간 낭비
    - NPM과 Yarn v1에서 오른쪽 트리와 같이 트리 모양 변경
    - 호이스팅에 따라 직접 의존하고 있지 않은 라이브러리를 `require()`할 수 있는 현상 : [유령 의존성](https://rushjs.io/pages/advanced/phantom_deps/)
    - `package.json`의 수정에 따라 의존성 관리 시스템이 혼란스러워질 가능성 ⬆️

## 2️⃣ 본론 2 - 왜 Yarn Berry인가?(2)
`Yarn Berry`는 위에서 언급한 `NPM`의 "깨져 있는" 패키지 관리 시스템을 개선하고자    
적은 공간의 사용, 효율적인 의존성 검색을 목표로 출시되었다.   

### ▶️ PnP (Plug'n'Play)
`node_modules` 폴더의 특정 패키지를 검색할 경우 모든 패키지를 순회하며 해당 패키지 존재 여부를 찾는 방법은 매우 비효율적이다.   
1. `Node`가 **패키지를 검색할 때 잘 찾을 수 있도록 도와주는 역할**이 패키지 매니저의 일이라는 생각과   
2. 패키지 매니저가 `node_modules` 디렉터리 구조를 만드는 것에 그치지 않고, 보다 **근본적이며 안전한 방법으로 의존성을 관리**하는 방법에 대해 고민한 결과
Plug'n'Play가 탄생했다.   

`Yarn Berry`에서는 `node_modules`를 생성하는 대신 의존성 lookup 파일인 `.pnp.cjs`를 생성한다.   
- `.pnp.cjs` 파일의 포함 내용
    - 관련된 패키지 이름
    - 패키지 버전
    - 디스크에서의 위치
    - 의존성 리스트
    - etc.
<br>

- **`Plug'n'Play` 켜기**
`NPM`에서 최신 버전의 `Yarn`을 내려받은 뒤, 버전을 `Berry`로 설치해 `Yarn Berry`를 사용한다.
```cmd
$ npm install -g yarn
$ cd ../path/to/some-package
$ yarn set version berry
```
`Yarn Berry`는 하위호환을 위해 **패키지 단위**로만 의존성 관리 시스템을 도입할 수 있다.   
`node_modules`를 생성하지 않는 `Yarn Berry`는 의존성 정보를 `.yarn/cache` 폴더에 저장한다.   
`.pnp.cjs` 파일에 의존성을 찾을 수 있는 정보가 기록되며, 해당 파일을 통해 Disk I/O 없이 어떤 패키지가 어떤 라이브러리에 의존하는지, 각 라이브러리가 어디에 위치하는지 바로 알 수 있다.   

`Yarn`은 `Node.js`에서 제공하는 `require()`문의 동작을 덮어씀으로써 효율적으로 패키지를 검색할 수 있도록 한다.    
- `PnP API`를 이용해 의존성 관리를 하고 있을 경우 : `yarn node`명령어를 사용 (`node` 명령어 X)   

`Node.js` 앱을 실행 시 `package.json`의 `scripts`에 실행 스크립트를 등록해 사용한다.    
`Yarn`으로 스크립트를 실행하면 PnP로 의존성을 자동으로 불러온다.    

또한 **Zip 아카이브로 의존성**을 관리할 수 있는데 Zip 아카이브를 사용할 경우,     
없는 의존성이나 더 이상 필요없는 의존성을 쉽게 찾을 수 있다.   
Zip 파일의 내용이 변경될 경우 체크섬과 비교해 쉽게 변경 여부를 감지할 수 있다.   

## ▶️ 본문 - Yarn PnP 도입의 이점
1. **의존성 검색**
    - 의존성 검색 시 더 이상 `node_modules` 폴더의 순회가 필요 없다.
    - `.pnp.cjs`파일이 제공하는 자료구조를 이용해 의존성의 위치를 바로 찾는다. 
    - `require()`에 걸리는 시간이 크게 단축된다.

2. **재현 가능성**
    - 패키지의 모든 의존성이 `.pnp.cjs` 파일을 이용해 관리되기에 더 이상 외부 환경에 영향받지 않는다.

3. **의존성을 설치할 때**
    - 설치를 위한 `node_modules` 디렉토리 생성이 필요없다.
    - `zero-install` 사용 시 대부분의 라이브러리를 설치할 필요 없이 사용 가능하다.
    - 같은 버전의 패키지가 여러번 복사될 필요가 없기에 설치 시간을 극단적으로 단축할 수 있다. 

4. **엄격한 의존성 관리**
    - `node_modules`와 같이 의존성을 끌어올리지 않는다.
    - 각 패키지가 자신이 `package.json`에 기술하는 의존성에만 접근할 수 있다.
    - 예기치 못한 버그를 일으키는 유령 의존성 현상을 막을 수 있다. 

5. **의존성 검증**
    - `Yarn PnP`에서 Zip파일을 이용해 패키지를 관리하므로 의존성 관리가 용이하다.
    - 의존성이 잘못되었을 때 쉽게 바로잡을 수 있다.

6. **Zero-Install**
    - `Zero-Install` : `Yarn Berry`에서 의존성을 버전 관리에 포함하는 것
    - `Yarn PnP`는 의존성을 압축 파일로 관리하므로 의존성 용량이 작다.
    - Git으로 의존성을 관리할 수 있다.
        - 새로 저장소를 복제하거나 브랜치를 바꿀 경우에도 `Yarn install`을 실행하지 않아도 된다.
        - 네트워크가 끊어진 곳에서 **오프라인 캐시**기능을 사용할 수 있다.
        - CI에서 의존성을 설치하는 시간을 절약할 수 있다.
    - `Zero-Install` 사용 시 `.gitignore` 파일 설정
    ```
    .yarn/*
    !.yarn/cache
    !.yarn/patches
    !.yarn/plugins
    !.yarn/releases
    !.yarn/sdks
    !.yarn/versions
    ```

## ▶️ Yarn Berry의 단점
1. **여전히 PnP를 지원하지 않는 패키지 존재**
    - 프로젝트에 PnP를 지원하지 않는 패키지가 하나라도 존재한다면 PnP 방식일지라도 `node_modules`가 따라온다.
        - PnP를 지원하지 않는 패키지가 있을 경우,
            - sol 1) 버전 올리기
            - sol 2) 다른 패키지로 이전하기
            - sol 3) PnP를 지원하도록 기여하기
    - 각 모듈이 PnP로 사용될 수 있기 위해서는 PnP 방식에 맞게 의존성 관리가 strict하게 셋팅되어야 한다.
        - PnP loose 모드를 통해 명시적으로 요구하는 디펜던시를 요구하지 않도록 할 수 있다.
        ```yml
        // .yarnrc.yml

        pnpMode: loose
        ```

## 📌 자료 출처 & 함께 보면 좋을 자료
- [node_modules로부터 우리를 구원해 줄 Yarn Berry](https://toss.tech/article/node-modules-and-yarn-berry)
- [yarn berry로 React.js 프로젝트 시작하기](https://kasterra.github.io/setting-yarn-berry/)
- [Yarn Berry를 사용해보자](https://velog.io/@seokunee/Yarn-Berry%EB%A5%BC-%EC%82%AC%EC%9A%A9%ED%95%B4%EB%B3%B4%EC%9E%90)
- [yarn berry의 이점](https://velog.io/@oimne/yarn-berry)
- [패키지 관리자 Yarn berry 알아보기](https://velog.io/@ragnarok_code/Yarn-berry)
- [Yarn Berry, 굳이 도입해야 할까?](https://medium.com/teamo2/yarn-berry-%EA%B5%B3%EC%9D%B4-%EB%8F%84%EC%9E%85%ED%95%B4%EC%95%BC-%ED%95%A0%EA%B9%8C-d6221b9beca6)
- [자바스크립트 의존성 지옥](https://yceffort.kr/2020/11/javascript-dependency-hell)
- [[Yarn berry] pnp(Plug And Play), Zero Install을 위한 Dependency 문제 해결하기](https://helloinyong.tistory.com/341)