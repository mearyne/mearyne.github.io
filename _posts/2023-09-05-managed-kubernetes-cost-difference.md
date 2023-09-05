---
title: GKE, AKS, EKS 가격비교
date: 2023-09-05 10:18:10 +0900
categories: [MSA, Kubernetes]
tags: [msa, kubernetes, gks, aks, eks]     
---

## 결론

|              |   AKS   |   GKS   |   EKS   |
| ------------ | ------- | ------- | ------- |
| 1시간당 가격 | 0.1달러 | 0.1달러 | 0.1달러 |

## AKS 가격

![aks-price](https://raw.githubusercontent.com/mearyne/mdImgHost/master/_posts/2023-09-05-managed-kubernetes-cost-difference.md/252981910254186.png)
1클러스터 기준 시간당 0.1달러
1달러 = 1321.9999 원
1달 = 30일 = 720시간 기준으로 계산시 95,184원



![무료 체험](https://raw.githubusercontent.com/mearyne/mdImgHost/master/_posts/2023-09-05-managed-kubernetes-cost-difference.md/203663715245509.png)

1달 무료 체험 기능 제공



## EKS 가격

![EKS-price](https://raw.githubusercontent.com/mearyne/mdImgHost/master/_posts/2023-09-05-managed-kubernetes-cost-difference.md/343992910240866.png)

1클러스터 기준 시간당 0.1달러  
절약 플랜 사용시 1년 13% 할인  
절약 플랜 사용시 3년 32% 할인  

1클러스터, Amazon EKS 옵션 선택 = 월 73.00 USD, 년 876.00 USD(할인 안된 가격)




## GKE 가격

![GKE-Price](https://raw.githubusercontent.com/mearyne/mdImgHost/master/_posts/2023-09-05-managed-kubernetes-cost-difference.md/251415915234807.png)

시간당 0.1달러
월 744시간 기준 월별 74.4 달러




## 참고사이트
1. [aks price](https://azure.microsoft.com/ko-kr/pricing/details/kubernetes-service/)  
AKS 가격

2. [eks price](https://aws.amazon.com/ko/eks/pricing/)  
EKS 가격

3. [gks price](https://cloud.google.com/kubernetes-engine/pricing?hl=ko)  
GKE 가격