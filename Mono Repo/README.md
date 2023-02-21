<<<<<<< HEAD
# Front-End Development PlayGround 🎠
Web FE 생태계에는 새로운 패러다임과 기술들이 매우 빠르게 등장하고 있습니다.   
따라서 학습하고자 하는 패러다임과 기술들에 대한 자료들을 아카이빙하고, 시도 및 적용해보며   
최종적으로 가독성있는 문서로 정리해 공유하는 과정을 통해 성장하는 것을 목표로 합니다.    
관심있는 주제가 생길 때마다 Contents가 추가됩니다.   

### 💡 Contents
- [Package Manager](https://github.com/yoo-jimin127/FrontEnd-PlayGround/blob/main/Package%20Manager/README.md)
    - [NPM](https://github.com/yoo-jimin127/FrontEnd-PlayGround/blob/main/Package%20Manager/01_NPM.md)
    - [Yarn classic](https://github.com/yoo-jimin127/FrontEnd-PlayGround/blob/main/Package%20Manager/02_YARN-classic.md)
    - [PNPM](https://github.com/yoo-jimin127/FrontEnd-PlayGround/blob/main/Package%20Manager/03_PNPM.md)
    - [Yarn berry](https://github.com/yoo-jimin127/FrontEnd-PlayGround/blob/main/Package%20Manager/04_YARN-berry.md)
- Bundler
    - Webpack
    - RequireJS
    - Browserify
    - Rollup
    - Parcel
- FrontEnd Rendering
    - CSR(Client Side Rendering)
    - SSR(Server Side Rendering)
- React
    - RSC(React-Server-Component)
    - Suspense
    - Error Boundary
- CI/CD
- Storybook
- Monorepo
- Statement Management
    - Redux
    - RTK(Redux ToolKit)
    - Recoil
    - React query
    - SWR(State While Revalidate)
    - mobX
    - zustand
    - zotai

### 👩🏻‍💻 Writer
<img src="https://contrib.rocks/image?repo=yoo-jimin127/FrontEnd-PlayGround" /><br>
<a href="https://github.com/yoo-jimin127"><b>Jimin Yoo(yoo-jimin127)</b></a>

처음 접하고 공부하는 내용이 많아 잘못된 부분이 있을 수 있습니다.   
오타 및 오류 내용에 대한 피드백은 대환영입니다!🙆🏻‍♀️    
[issue](https://github.com/yoo-jimin127/FrontEnd-PlayGround/issues)에 남겨주세요!   
=======
# Mono Repo
> 버전 관리 시스템에서 두 개 이상의 프로젝트 코드가 동일한 저장소에 저장되는 소프트웨어 개발 전략   

모노레포의 개발 전략은 기존 [모놀리식 애플리케이션](https://glossary.cncf.io/ko/monolithic-apps/)에 대한 비판으로부터 비롯되었다.   

## ✅ 모놀리식 애플리케이션
- 단일 코드 베이스의 애플리케이션
- 전체 애플리케이션은 단일 코드로 작성되어 단일 데이터베이스에 접근
- 단독으로 배포 가능한 프로그램에 모든 기능을 포함하는 형식

<img src="https://user-images.githubusercontent.com/66112716/219326972-de0101fe-42e5-4764-894f-e0ef8d91219a.png" width="800" />

[image reference](https://www.suse.com/c/rancher_blog/microservices-vs-monolithic-architectures/)

### ▶️ 모놀리식 애플리케이션의 장단점
- **장점**
    - 단순성 : 모든 코드는 단일 코드 베이스에 존재 (로컬에서의 실행 시 단일 애플리케이션만 실행)
    - 간편한 배포 : 단일 프로젝트로 배포
    - 보편성 : 대부분 모놀리식 아키텍쳐에 대한 개발 경험 존재
    - 쉬운 디버깅 : 모든 코드가 단일 애플리케이션에 있으므로 쉬운 디버깅
    - 쉬운 테스트 : 모든 코드가 단일 애플리케이션에 있으므로 쉬운 테스트
    - 쉬운 모니터링 : 단일 프로젝트에 모든 코드가 존재하기에, 오류 시 문제 발생 위치 식별 용이

- **단점**
    - 규모가 커질수록 증가하는 유지보수의 어려움
    - 유연하지 않은 확장성
    - 대규모 팀 작업의 어려움
    - 기술 사용의 제한

💡 코드가 서로 직접적으로 의존하고 있기에 단 하나의 버전으로 관리된다.    
따라서 **관심 분리**가 어려워지며, 설계, 리팩터링, 배포 등의 작업을 매번 거대한 단위로 처리해야하므로 많은 비용이 발생한다.   

## ✅ 모노레포
두 개 이상의 프로젝트가 동일한 저장소에 저장되는 소프트웨어 개발 전략   


## 📌 참고 자료
- https://yozm.wishket.com/magazine/detail/1813/
>>>>>>> 2ab044d (init : yarn berry init)