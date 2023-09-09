---
title: ioc 컨테이너에 있는 Bean 리스트 확인하는 법
date: 2023-09-09 09:49:48 +0900
categories: [java, Spring]
tags: [ioc, container, bean]     
---

```java
package shop.mtcoding.bank;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.context.ConfigurableApplicationContext;

@SpringBootApplication
public class BankApplication {

	public static void main(String[] args) {
		ConfigurableApplicationContext context = SpringApplication.run(BankApplication.class, args);
		String[] iocNames = context.getBeanDefinitionNames();
		for (String iocName : iocNames) {
			System.out.println(iocName);
		}

	}

}
```

![ioc-container-bean-list](https://raw.githubusercontent.com/mearyne/mdImgHost/master/_posts/2023-09-09-ioc-container.md/305536315133070.png)

내가 수정한 Bean이 제대로 등록이 됐는지를 확인하고 싶을때 사용하면 좋을 듯 싶다.  
요즘들어 Security라던지, Bean을 등록할 일이 있었는데 제대로 작동이 안되는 일이 잦았다. 그때 이걸 사용하면 좋을듯.  
근데 굳이 이렇게까지 해서 확인할 필요가 있을까 싶긴 하다. 그냥 해당 @Bean에다 log를 찍어보면 간단하게 확인이 가능하기 때문에...  
교차검증에 의미가 있을듯 싶다.  