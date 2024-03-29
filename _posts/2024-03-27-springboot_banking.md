---
layout: single
title: "spring_banking"
categories: java
tag: spring_banking
toc: true
---

# spring_banking

- client table 구조
- entity로 @Column으로 지정안해도 타입까지 컬럼 생성됨 

```
@Data
@AllArgsConstructor
@NoArgsConstructor
@Table(name = "accounts")
@Entity
public class Account {
	@Id
	@GeneratedValue(strategy = GenerationType.IDENTITY)
	private Long id;
	
	@Column(name = "account_holder_name")
	private String accountHolderName;
	
	private double balance;	
}
```



