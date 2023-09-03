---
title: MMA 연결 안됨 문제
date: 2023-09-03 23:06:44 +0900
categories: [Game, Arknights]
tags: [arknights, game]     
---

## 문제
docker-desktop 연결 안됨에 따라서 하이퍼바이저 윈도우 설정을 좀 만진 것 때문인지,  
아니면 업데이트 때문인지 알 수는 없지만 연결이 안되기 시작했다.  
환경은 윈도우10 블루스택 Pie64비트이다.  




## 해결
멀티인스턴스 관리자에 들어갔을때 내가 주로 사용하는 인스턴스는 Pie 64비트이다.  
해당 버전은 Hyper-V 버전이기 때문에 공식홈페이지에 있는 Hyper-V 버전 해결책을 찾았다.  

0. MAA 끄기
1. MAA 설치 폴더에서 gui.json 파일을 찾는다
2. Bluestacks.Config.Path를 Default 안에 넣는다.
```
{
    "Configurations": {
        "Default": {
            "Bluestacks.Config.Path":"C:\\ProgramData\\BlueStacks_nxt\\bluestacks.conf",
            // ...
        }
    }
}
```
3. MAA 재시작 후 재연결

이제부터 제대로 작동되기 시작한다.    
역시 공식문서에 답이 있었다...  

블루스택 자체가 여러 버전이 존재하고, 또 어떤 곳은 재시작만으로 해결이 됐다는 곳도 있었고, 어떤 곳은 관리자 모드로 켜야지 됐다는 사람도 있다.  
환경따라 많이 달라지므로 이것도 저것도 다 해봤는데 만약 안된다면 처음부터 다시 설치하는게 속 편하지 않을까 싶다..  



## 참고사이트
1. [maa 공식문서](http://maa.plus/docs/ko-kr/1.3-에뮬레이터_지원.html)