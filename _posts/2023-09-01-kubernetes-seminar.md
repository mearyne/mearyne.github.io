---
title: kubernetes 세미나
date: 2023-09-01 15:34:17 +0900
categories: [MSA, kubernetes]
tags: [kubernetes, msa, docker-compose, docker-desktop, 관리형쿠버네티스]     
---


## 1. 주요 개념
### 도커 (Docker) 
- 프로그램이나 서버를 격리시키는 기능을 제공하는 소프트웨어.  
- `Docker Engine`이 있어야지 컨테이너를 생성하고 구동시킬 수 있다.  
- 컨테이너를 만들려면 `이미지`가 필요하다.
- 도커는 리눅스에서 사용한다. 윈도우, 맥에서 사용하는 도커는 리눅스가 포함된 패키지(docker desktop)를 다운받는다.

`이미지` : 빵틀  
`컨테이너` : 실제 빵  

하나의 이미지, 하나의 컨테이너, 여러개의 서비스

하나의 컨테이너는 일회용품에 가깝다. 하나를 두고두고 써먹는 것이 아닌, 새로운 버전이 생긴다면 기존 것을 폐기하고 새로운 것을 만드는 방식이다.  



### Docker Desktop 
: 애플리케이션을 쉽게 생성, 개발 및 테스트할 수 있는 툴  
도커를 사용하기 위해서는 리눅스가 필요하다. 따라서 도커를 사용하기 위해서는 어떠한 형태로든(VMware, VirtualBox, WSL2, Hyper-V...etc) 설치하고 그 위에 도커가 위치하게 된다.  
docker desktop은 다음과 같은 요소를 포함하고 있다.  

| 윈도우용    | mac용     |
| --- | --- |
| 도커엔진    | 도커엔진     |
| 리눅스 운영체제    | 리눅스 운영체제     |
| Hyper-V    | 가상환경(Hyper-Kit)    |

도커를 간단하게 설치해주는 툴이라 볼 수 있다.  
도커 데스크탑을 설치할때 WSL2 또는 Hyper-V 중에서 어떤걸 사용할지 선택하는 것이 존재한다.  
도커 제작사가 제공하는 리눅스를 사용해도 되지만(docker desktop에 내장되어있다) WSL2를 권장한다.  

> docker는 32비트에서는 작동되지 않는다. 64비트에서만 작동된다.
{: .prompt-info }


### docker-compose 
: 이미지들을 일괄적으로 실행해줌  
시스템 구축과 관련된 명령어를 하나의 텍스트 파일(docker-compose.yaml)에 기재해 명령어 한번에 시스템 전체를 실행하고 종료와 폐기까지 한번에 하도록 도와주는 도구.  
싱글 호스트에서 작동된다.  




### 쿠버네티스 (Kubernetes) 
: 컨테이너를 관리하는 툴  
컨테이너 오케스트레이션 도구의 일종이다.  
쿠버네티스는 여러 대의 물리적 서버가 존재하는 것을 전제로 한다(하나하나의 물리적 서버는 여러 대의 컨테이너를 실행한다).  
쿠버네티스는 컨테이너를 '바람직한 상태를 유지'하는 것이지 수동으로 삭제하거나 그러는 것은 바람직하지 않다.  
(직접 삭제하더라도 마스터 노드는 컨테이너가 부족하다고 판단하여 자기 멋대로 추가할 것이기 때문에)

![songdo-IDC](https://raw.githubusercontent.com/mearyne/mdImgHost/master/_posts/2023-09-01-kubernetes-seminar.md/333567829951540.png)

> `컨테이너 오케스트레이션` : 시스템 전체를 총괄하고 여러 개의 컨테이너를 관리하는 일을 말한다.  




### 관리형 쿠버네티스 (Managed Kubernetes) 
: 쿠버네티스를 대신 관리해주는 툴  
AKS(Azure), EKS(AWS), GKE(GCP) 등이 존재한다.  

![managed kuberneetes](https://raw.githubusercontent.com/mearyne/mdImgHost/master/_posts/2023-09-01-kubernetes-seminar.md/520354223586586.png)



## 2. docker-compose vs 쿠버네티스 비교
### 1. Multi-Node Management
도커 컴포즈는 single host system에서 컨테이너가 실행된다.
쿠버네티스는 멀티노드(컴퓨터)로 배포된다. sacle-in, sacle-out 에 도움이 된다.

### 2. Pod Architecture
쿠버네티스는 Pod Architecture를 따른다.
쿠버네티스의 서비스는 Pod의 집합이라 부른다.

![pod architecture](https://raw.githubusercontent.com/mearyne/mdImgHost/master/_posts/2023-09-01-kubernetes-seminar.md/259263494899944.png)

### 3. Auto-Scaling
쿠버네티스는 수평적 확장이 용이하다.

### 4. self-Healing Containers
컨테이너에 이상이 생겼을때 자동으로 회복을 시켜준다.

### 결론
도커 컴포즈는 배포에만 영향을 끼칠 수 있다. 그 이후의 것은 신경쓸 수 없다(쓰지도 않는다).  
쿠버네티스는 배포 이후의 것들에 영향을 끼친다.  
쿠버네티스는 컨테이너 관리 도구이다. 그에반에 도커 컴포즈는 생성, 삭제를 하는 도구이다.    
또한 도커 컴포즈는 하나의 하드웨어에서만 작동하지만, 쿠버네티스는 여러 컴퓨터를 동시에 제어한다.  



## 3. Docker Desktop에서 쿠버네티스 세팅 가능 여부와 장점
![kubernetes in docker](https://raw.githubusercontent.com/mearyne/mdImgHost/master/_posts/2023-09-01-kubernetes-seminar.md/188954715255365.png)

- 설치가 간편
- 개인 사용자가 쿠버네티스를 익히는데 좋다




## 4. 쿠버네티스 관리 방법 비교 (직접 관리 vs 관리툴)
### 자체 서버환경에서 설치했을때 장점
서버 인프라를 미세하게 설정할 수 있다.
클라우드에서 지원하지 못하는 기능이 필요하다면 자체 구축을 고려해야 함.
모든 관리를 직접 해야 하기 때문에 운영, 관리가 복잡해진다.


### 2. 관리툴 이용
설치가 필요없다.
쉽게 사용이 가능하고, 각 관리툴의 자체적인 기능 활용이 가능함.
도입 전에는 관리툴이 적합한지 확인하는 단계가 필요함.

- 클러스터를 구성하고 설치하는 데 시간 단축
- 클러스터 컨트롤 플레인이 자동으로 생성됨
- 배포 및 관리를 더 간소화
- 간단하게 클러스터 버전 업그레이드 및 Scale out이 가능함


### 그래서 어느걸 선택해?
쿠버네티스를 채택하는 것은 꽤 흔하지만 이를 직접 구축하는 것은 별개의 문제다. 대개는 외주로 구축을 맡긴다.  
- 서비스마다 부여되는 클러스터IP에 로드 밸런싱을 적용하기 위한 하드웨어 지식
- 드라이버 상성 문제
- 유지보수 난이도 문제





## 5. 쿠버네티스로 무중단 배포 방법과 그 이유
Rolling Update를 통해 무중단 배포가 가능하다.
(쿠버네티스의 무중단 배포에는 Rolling Update, blue-green, canary 세가지가 존재한다)
![rolling update](https://raw.githubusercontent.com/mearyne/mdImgHost/master/_posts/2023-09-01-kubernetes-seminar.md/177255115236606.png)
yaml 설정을 통해 가능하다



## 6. VMware Tanzu의 장단점과 활용 방법

> VMware(혹은 Virtual Box)는 가상의 물리 서버를 만든다. 실질적으로 물리 서버와 동일하므로 아무 것이나 설치할 수 있고, 어떤 소프트웨어를 구동해도 무방하다.
{: .prompt-info }

VMware Tanzu를 통한 애플리케이션 현대화.
기업에서 Kubernetes 기반으로 최신 애플리케이션을 구축하고 운영, 관리할 수 있도록 애플리케이션을 현대화해주는 최적의 솔루션이다.




- 코드를 통한 OS 및 인프라 설치를 통한 IAC 표준화 가능
- ClusterAPI를 통한 노드 스케일이 용이함(자동 API)
- 오픈소스 쿠버네티스와 비교했을때 호환성 부분에서 월등함
- `IAAS`, `PAAS`를 아우르는 벤더/파트너 기술지원
- Spring과 Tanzu의 연결성을 통한 Dev Experience 제공
- 하이브리드 클라우드/ 멀티 클라우드에 가장 적합한 쿠버네티스 플랫폼
- VMware 기술 요소와의 완벽한 결합


> IAAS? PAAS?
> Infrastructure as a service : 서비스로 제공하는 인프라스트럭쳐
> Platform as a service : 개발사에 제공되는 플랫폼
> ![iaas_vs_paas](https://raw.githubusercontent.com/mearyne/mdImgHost/master/_posts/2023-09-01-kubernetes-seminar.md/427983515242379.png)




## 번외. Spring cloud vs kubernetes

참고 : https://developers.redhat.com/blog/2016/12/09/spring-cloud-for-microservices-compared-to-kubernetes


MSA에서의 문제는 다음과 같다.
- Config Management
- Service Discovery & LB
- Resilience & Fault Tolerance
- API Management
- Service Security
- Centralized Logging
- Cetralized Metrics
- Distributed Tracing
- Scheduling & Deployment
- Auto Scaling & Self Healing


![spring_cloud_vs_kubernetes](https://raw.githubusercontent.com/mearyne/mdImgHost/master/_posts/2023-09-01-kubernetes-seminar.md/62893615260259.png)

### 차이점
- ribbon -> kubernetes service
- zuul -> kkubernetes serrvice & ingress resources
- eureka -> kubernetes service & ingress resources
- hystrix -> kubernetes health check & resource isolation


#### Spring Cloud의 장단점
- 손쉬운 구축. 시작이 빠르다
- 다양한 라이브러리 존재
- 라이브러리끼리 서로 잘 통합되어있음

- Java로만 제한된다
- Java 애플리케이션이 처리해야 할 책임이 너무 많다
- Spring Cloud만으로는 부족한 MSA 구축영역(자동화된 배포, 일정 관리, 리소스 관리, 프로세스 격리, 자가 치유, 파이프라인 구축 등)


#### Kubernetes 장단점
- 언어에 구애받지 않는 컨테이너 관리 플랫폼
- Spring cloud보다 좀더 광범위한 MSA 문제를 해결한다.

- 모든 언어에서 사용할 수 있기에 개별 언어에 대해서는 최적화가 되어있지 않다
- Kubernetes는 개발자가 아닌 DevOps 중심의 플랫폼이다.
- 비교적 새로운 플랫폼(2년차), 빠르게 많은 것들이 변함

![springcloud and kubernetes strength and weakness](https://raw.githubusercontent.com/mearyne/mdImgHost/master/_posts/2023-09-01-kubernetes-seminar.md/342133615257863.png)


## 참고 사이트

1. [왜 매니지드 쿠버네티스인가요?](https://www.cloocus.com/insight-kubernetes_2/)    
2. [그림과 실습으로 배우는 도커 & 쿠버네티스](https://www.yes24.com/Product/Goods/108431011)  
