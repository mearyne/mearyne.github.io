---
title: GKE, AKS, EKS 가격비교
date: 2023-09-05 10:18:10 +0900
categories: [MSA, kubernetes]
tags: [msa, kubernetes, gks, aks, eks]     
---

## 결론

|              |   AKS   |   GKS   |   EKS   | VMware Cloud on AWS(tanzu) | VMware Tanzu Application Platform |
| ------------ | ------- | ------- | ------- | -------------------------- | --------------------------------- |
| 1시간당 가격 | 0.1달러 | 0.1달러 | 0.1달러 | 8.34달러                    | 문의필요                           |

## AKS 가격

![aks-price](https://raw.githubusercontent.com/mearyne/mdImgHost/master/_posts/2023-09-05-managed-kubernetes-cost-difference.md/252981910254186.png)
1클러스터 기준 시간당 0.1달러
1달러 = 1321.9999 원
1달 = 30일 = 720시간 기준으로 계산시 95,184원





## EKS 가격

![EKS-price](https://raw.githubusercontent.com/mearyne/mdImgHost/master/_posts/2023-09-05-managed-kubernetes-cost-difference.md/343992910240866.png)

1클러스터 기준 시간당 0.1달러  
절약 플랜 사용시 1년 13% 할인  
절약 플랜 사용시 3년 32% 할인  





## GKE 가격

![GKE-Price](https://raw.githubusercontent.com/mearyne/mdImgHost/master/_posts/2023-09-05-managed-kubernetes-cost-difference.md/251415915234807.png)

시간당 0.1달러



### tanzu 가격

Azure VMware Solution : 가격 문의 필요함  
Google Cloud VMware Engine : 한국 서버 없음  
VMware Cloud on AWS : 아래 사진과 같다  
위 세가지의 관리툴과는 다르게 통합적으로 기능을 제공한다.  
클라우드 네이티브 애플리케이션을 개발하기 위한 VMware Tanzu Application Platform 제품의 경우 별도 사용이 가능여부와 가격은 별도 메일문의가 필요하다.  


![vmware cloud on aws](https://raw.githubusercontent.com/mearyne/mdImgHost/master/_posts/2023-09-05-managed-kubernetes-cost-difference.md/120203716230946.png)

옵션1. i3.metal : 용량과 사양이 제일 낮다  
1시간당 8.34달러(월별구독)  


옵션2. i3en.metal : 용량이 제일 많고 사양도 중간이다  
1시간당 16.26달러(월별구독)  
1시간당 14.57달러(연구독)  
1시간당 8.76달러(3년구독)  


옵션3. i4i.metal : 사양이 좋으나 옵션2보다 용량이 좀 낮다  
1시간당 15.51달러(월별구독)  
1시간당 11.00달러(연구독)  
1시간당 9.64달러(3년구독)  


## 참고사이트
1. [aks price](https://azure.microsoft.com/ko-kr/pricing/details/kubernetes-service/)  
AKS 가격  

2. [eks price](https://aws.amazon.com/ko/eks/pricing/)  
EKS 가격  

3. [gks price](https://cloud.google.com/kubernetes-engine/pricing?hl=ko)   
GKE 가격  

4. [tanzu 가격](https://www.vmware.com/kr/products/vmc-on-aws/pricing.html)  
VMware Cloud on AWS 가격