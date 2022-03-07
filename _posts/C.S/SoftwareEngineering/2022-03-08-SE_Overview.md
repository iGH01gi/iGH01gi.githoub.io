---
layout: post
title: 소프트웨어 공학이란
date: 2022-03-08 00:00:00+0900
category: SoftwareEngineering
published: true
---
# 소프트웨어공학의 탄생  
1968년 독일 garmisch에서 열린 첫번째 NATO Software Engineering Conference에서 탄생.  
정확하고 이해할수있고 입증할수 있는(신뢰) 컴퓨터 프로그램을 짜는것의 어려움에 의해서 나오게 됨.  

---

# 소프트웨어공학에서 다루는 주요 주제들

### 소프트웨어 개발 과정 
- 요구 분석 및 상세화  
- 소프트웨어 모델링  
- 소프트웨어 아키텍쳐&디자인  
- 소프트웨어 개발(코딩)  
- 소프트웨어 검증

### 프로젝트 관리
- 조직 관리, 툴, 리스크 관리  
- 예측,스케쥴링,계획  
- 품질  

### 버전 관리


<br><br><br>
즉, 소프트웨어가 생산되는 **과정**에 대한 것.  

---

# 다른 공학과 구별되는 SW의 특성  

### - invisible하다
눈에 직접적으로 보이지 않기 때문에 이해하고, 분석하고, 평가하는데 어려움이 있다.  

### - SW의 Failure Rate는 다른 분야와 다르다!
![일반적인FailureRate](\images\SoftwareEngineering\FailureRate1.png)  
일반적인 공학분야(ex.토목,기계 등등..)는 위와같이 초기 개발단계에서는 오류가 많지만 실사용단계로 오면 그 정도가 줄어들고 평이해진다. (바뀌는 경우가 거의 없기때문.)  
그리고 시간이 지나면 노후 등으로 인하여 결점이 생기고 Failure Rate의 상승으로 이어지게 된다. 

![SW의FailureRate](\images\SoftwareEngineering\FailureRate2.png)  
반면 SW분야는 소프트웨어이기 때문에 노후로 인한 문제가 없는 대신 실사용단계에서 업데이트등으로 인하여 그 구조가 작든,크든 변하는 경우가 자주 있고 그로 인하여 Failure Rate도 종종 상승하게 된다. 따라서 이 구간을 관리해줄 필요가 있다.  

### - SW의 개발 기간은 투입인력과 비례하지 않는다
![man-month](\images\SoftwareEngineering\manmonth.png)  
건축분야를 예로 들면 큰 규모의 건축을 할 때 현장 인력이 많으면 많을수록 건설 기간이 줄어들게 된다.(좌측)  
그러나 SW분야는 어느 정도까지는 기간이 단축이 되다가 일정 인원이 넘어가면 오히려 증가하게 되는 결과로 이어진다.(우측)  
브룩스의 법칙이라고도 불리는 것인데 이는 SW개발에 필요 이상의 인력이 투입되면 각 팀 간의 **의사소통 비용이 증가**하게 되어서 문제를 더 크게 만들 수 있다는 것 이다.  
잘못 해석할 여지가 많은 말이기에 나름대로 잘 해석할 필요가 있어 보인다.  

---

# 소프트웨어 개발 과정에 대한 간략한 overview  

### [소프트웨어 개발 프로세스]
소프트웨어 개발 프로세스는 작업 산출물을 정의할 뿐만 아니라 그들의 순서와 빈도를 표현함으로써 활동들 간의 상호 관계를 규정한다.  

### [소프트웨어 모델링]
- 모델=시스템의 추상화 
- 모델링은 관련 없는 세부 사항을 무시하여 복잡성을 해결할 수 있는 방법이다.  
- 고객, 시스템 분석가 및 프로그래머 간에 시스팀 분석 및 디자인의 결과와 아이디어를 공유하는 것  
- **Unified Modeling Language(UML)**: 통합 모델링 언어는 소프트웨어 공학에서 사용되는 표준화된 범용 모델링 언어이다. 객체 지향 프로그래밍 소프트웨어 집약 시스템을 개발할 때 산출물을 명세화, 시각화, 문서화할 때 사용한다.  

### [소프트웨어 아키텍쳐]  

- 시스템이 구축되면 변경하기 어렵거나 불가능한 문제에 초점을 맞춘다.(e.g. performance, reliability, scalability...)  
- **큰 그림 그리기!**

### [소프트웨어 디자인]

**소프트웨어 디자인의 중요 컨셉**  
- 추상화  
- 캡슐화  
- Separation of Concerns(SOC)
- 인터페이스
- 모듈화 

**측정**
- Cohesion (the degree to which the elements inside a module belong together)
- Coupling (degree of interdependence between software modules)

**객체지향 설계 5원칙**
-SOLID (SRP, OCP, LSP, ISP, DIP)

### [검증(Verification & Validation)]  
- 테스트 (black-box , white-box 테스트)  

![테스팅](\images\SoftwareEngineering\testing.png)