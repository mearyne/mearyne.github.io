---
title: kubernetes 개념 공부
date: 2023-08-31 00:30:00 +0900
categories: [MSA, kubernetes]
tags: [msa, kubernetes, devops]     
---


[docker desktop을 사용하여 kubernetes를 사용해보자](https://mydailylogs.tistory.com/120)  
kubectl 명령어를 사용해서 Api-Server로 명령(command)을 내린다

# dashboard 설치
CLI만을 이용하는 것이 아닌 GUI를 활용해서 Kubernetes를 사용해보자.
- 공식 사이트에서 제공하는 yaml을 이용해 dashboard 설치
- kubectl proxy를 사용해 dashboard 활성화
- http://localhost:8001/api/v1/namespaces/kubernetes-dashboard/services/https:kubernetes-dashboard:/proxy/#/login 해당 경로로 dashboard 접속
- 로그인을 위해서 계정 생성 -> 권한 설정 -> 토큰 발급 후 dashboard에 로그인하기


# 배포하기
dockerfile을 이용하여 이미지 만들기
docker에 이미지 push
쿠버네티스 배포파일(deployment.yaml) 생성


# 참고 사이트
1. [쿠버네티스 쉽게 이해하기](https://happycloud-lee.tistory.com/246)  
   쿠버네티스를 설치, 배포, 개념, 서비스 로드 밸런서 인그레스, 헬스 체크, 인증, 인가, 무중단배포 .... 수많은 개념들을 다양하고 자세하기 설명하고 있다.  
   한마디로 끝판왕이라 볼 수 있다.  
   하지만 간단한 배포의 내용을 알고 싶을때는 적합하지 않을 수 있다. 그리고 어려운 용어가 많기 때문에 익히는데 수고가 더 생길 수 있다.  


2. [쿠버네티스-샘플-프로젝트-배포하기](https://velog.io/@mertyn88/쿠버네티스-샘플-프로젝트-배포하기)  
   간단하고 심플하게 docker 설치, docker-desktop을 이용한 kubernetes 설치, dashboard 설치 및 접근 방법 소개, 배포까지 설명이 되어있다.
> 아직 안봐서 잘 모른다.
