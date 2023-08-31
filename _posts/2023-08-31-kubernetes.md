---
title: kubernetes 개념 공부
date: 2023-08-31 00:30:00 +0900
categories: [MSA, kubernetes]
tags: [msa, kubernetes, devops]     
toc: true
---

# kubernetes 구조
kubectl 명령어를 사용해서 Api-Server로 명령(command)을 내린다

# dashboard 설치
CLI만을 이용하는 것이 아닌 GUI를 활용해서 Kubernetes를 사용해보자.
- 공식 사이트에서 제공하는 yaml을 이용해 dashboard 설치
- kubectl proxy를 사용해 dashboard 활성화
- http://localhost:8001/api/v1/namespaces/kubernetes-dashboard/services/https:kubernetes-dashboard:/proxy/#/login 해당 경로로 dashboard 접속
- 로그인을 위해서 계정 생성 -> 권한 설정 -> 토큰 발급 후 dashboard에 로그인하기

> 첫 접근에는 문제없이 가능하다. 하지만 재부팅 후 다음 토큰 발급부터 아이디?를 찾지 못하는 오류 발생
{: .prompt-danger }

# 배포하기
참고사이트 2번 내용을 정리함.

1. dockerfile을 이용하여 이미지 만들기
2. docker hub에 이미지 push
3. 쿠버네티스 배포파일(deployment.yaml) 생성 후 적용
```
 kubectl apply -f deployment.yaml
```
4. get all 명령어로 업로드 됐는지 확인
```
 kubectl get all
```
5. 외부(localhost로 접속할 수 있게) http 포트포워딩
```
 kubectl port-forward svc/yaml에서설정한서비스이름 접근할포트/해상서비스내부포트
```

> 굳이 kubernetes로 배포하는데 docker-hub로 올릴 필요가 있을까?
{: .prompt-danger }


# 참고 사이트
1. [쿠버네티스 쉽게 이해하기](https://happycloud-lee.tistory.com/246)  
   쿠버네티스를 설치, 배포, 개념, 서비스 로드 밸런서 인그레스, 헬스 체크, 인증, 인가, 무중단배포 .... 수많은 개념들을 다양하고 자세하기 설명하고 있다.  
   한마디로 끝판왕이라 볼 수 있다.  
   하지만 간단한 배포의 내용을 알고 싶을때는 적합하지 않을 수 있다. 그리고 어려운 용어가 많기 때문에 익히는데 수고가 더 생길 수 있다.  


2. [쿠버네티스-샘플-프로젝트-배포하기](https://velog.io/@mertyn88/쿠버네티스-샘플-프로젝트-배포하기)  
   간단하고 심플하게 docker 설치, docker-desktop을 이용한 kubernetes 설치, dashboard 설치 및 접근 방법 소개, 배포까지 설명이 되어있다.


3. [docker desktop을 사용하여 kubernetes를 사용해보자](https://mydailylogs.tistory.com/120)  
docker desktop 설치, kubernetes 설치, dashboard 설치, k9s 설치 과정을 보여준다.  
그 이후의 것은 없다.  

> `k9s`는 kubectl 대신 kubenetes를 더욱 쉽게 관리하도록 도와주는 툴 
{: .prompt-info }

![k9s](https://raw.githubusercontent.com/mearyne/mdImgHost/master/_posts/2023-08-31-kubernetes.md/52985409250000.png){: height="400px"}