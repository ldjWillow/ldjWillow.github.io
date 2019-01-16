---
title: junit测试Spring
copyright: true
date: 2019-01-16 10:54:55
categories: spring
tags: [测试,junit,spring]
---

在app.xml中配置

```
<bean name="date" class="java.util.Date"/>
```

测试类

```java
@RunWith(SpringJUnit4ClassRunner.class)
@ContextConfiguration(locations = { "classpath:applicationContext.xml" })
public class MyTest {
	@Autowired
	Date date;
	@Test
	public void hehe() {
		System.out.println(date.toLocaleString());
	}
}
```

