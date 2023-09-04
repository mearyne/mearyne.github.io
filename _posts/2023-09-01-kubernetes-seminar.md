---
title: kubernetes 세미나
date: 2023-09-01 15:34:17 +0900
categories: [MSA, kubernetes]
tags: [kubernetes, msa, docker-compose, docker-desktop, 관리형쿠버네티스]     
---


## 1. 주요 개념
도커 (Docker) : 코드를 이미지화(컨테이너화) 시켜서 실행하는 툴
쿠버네티스 (Kubernetes) : 컨테이너화된 이미지들을 관리하는 툴
docker-compose : 이미지들을 일괄적으로 실행해줌
관리형 쿠버네티스 (Managed Kubernetes) : 쿠버네티스를 관리해주는 툴
Docker Desktop : 애플리케이션을 쉽게 생성, 개발 및 테스트할 수 있는 툴


## 2. docker-compose vs 쿠버네티스 비교
### 1. Multi-Node Management
도커 컴포즈는 single host system에서 컨테이너가 실행된다.
쿠버네티스는 멀티노드(컴퓨터)로 배포된다. sacle-in, sacle-out 에 도움이 된다.

### 2. Pod Architecture
쿠버네티스는 Pod Architecture를 따른다.
쿠버네티스의 서비스는 Pod의 집합이라 부른다.

### 3. Auto-Scaling
쿠버네티스는 수평적 확장이 용이하다.

### 4. self-Healing Containers
컨테이너에 이상이 생겼을때 자동으로 회복을 시켜준다.

### 결론
도커 컴포즈는 배포에만 영향을 끼칠 수 있다. 그 이후의 것은 신경쓸 수 없다.
쿠버네티스는 배포 이후의 것들에도 영향을 끼칠 수 있다.



## 3. Docker Desktop에서 쿠버네티스 세팅 가능 여부와 장점
![kubernetes in docker](https://raw.githubusercontent.com/mearyne/mdImgHost/master/_posts/2023-09-01-kubernetes-seminar.md/188954715255365.png)

- 설치가 간편
- docker desktop에서 설치하는 kubernetes는 일부 기능에 제한이 있다(고 함)


## 4. 쿠버네티스 관리 방법 비교 (직접 관리 vs 관리툴)
쿠버네티스를 직접 관리하는 방법과 관리툴(EKS, AKS, GKE)을 사용하는 방법을 비교하며 장단점을 제시합니다.

참고 : https://www.cloocus.com/insight-kubernetes_2/

### 1. 자체 서버환경에서 설치했을때 장점
서버 인프라를 미세하게 설정할 수 있다.
클라우드에서 지원하지 못하는 기능이 필요하다면 자체 구축을 고려해야 함.
모든 관리를 직접 해야 하기 때문에 운영, 관리가 복잡해진다.



### 2. 클라우드 서버 인프라위에 직접 설치	
클라우드의 인프라(VM, Network 등) 위에 설치함으로서 인프라 관리를 CSP에 이관한다.
사용자 입장에서 쿠버네티스의 설치와 설정을 직접 하기 때문에 관리툴보다 자유로운 설정이 가능하다.
클라우드 내에서 클러스터를 구축하는 과정과 클러스터와 쿠버네티스를 연결하는 과정이 어려울 수 있다.


### 3. 관리툴 이용
설치가 필요없다.
쉽게 사용이 가능하고, 각 관리툴의 자체적인 기능 활용이 가능함.
도입 전에는 관리툴이 적합한지 확인하는 단계가 필요함.

- 클러스터를 구성하고 설치하는 데 시간 단축
- 클러스터 컨트롤 플레인이 자동으로 생성됨
- 배포 및 관리를 더 간소화
- 간단하게 클러스터 버전 업그레이드 및 Scale out이 가능함



## 5. 쿠버네티스로 무중단 배포 방법과 그 이유
Rolling Update를 통해 무중단 배포가 가능하다.
(쿠버네티스의 무중단 배포에는 Rolling Update, blue-green, canary 세가지가 존재한다)
![rolling update](https://raw.githubusercontent.com/mearyne/mdImgHost/master/_posts/2023-09-01-kubernetes-seminar.md/177255115236606.png)
yaml 설정을 통해 가능하다



## 6. VMware Tanzu의 장단점과 활용 방법

VMware Tanzu를 통한 애플리케이션 현대화.
기업에서 Kubernetes 기반으로 최신 애플리케이션을 구축하고 운영, 관리할 수 있도록 애플리케이션을 현대화해주는 최적의 솔루션이다.


참고 : https://themapisto.tistory.com/181
참고 : https://www.iroo.co.kr/?page_id=5854


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

# ![springcloud and kubernetes strength and weakness](https://raw.githubusercontent.com/mearyne/mdImgHost/master/_posts/2023-09-01-kubernetes-seminar.md/342133615257863.png)