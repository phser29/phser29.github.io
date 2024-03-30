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

- ui가 없는구조에서 static 메소드로 값 입력

```
public static Account mapToAccount(AccountDto accountDto) {
		Account account = new Account(
					accountDto.getId(),
					accountDto.getAccountHolderName(),
					accountDto.getBalance()
				);
			
		return account;
	}
```

- jpa 특성으로 쿼리 없이 CRUD 구현가능
- service 비즈니스 로직 입력

```
@Service
@AllArgsConstructor
public class AccountServiceImpl implements AccountService {
	
	private AccountRepository accountRepository;
	
	@Override
	public AccountDto creaeteAccount(AccountDto accountDto) {
		Account account = AccountMapper.mapToAccount(accountDto);
		Account savedAccount = accountRepository.save(account);
		return AccountMapper.mapToAccountDto(savedAccount);
	}	
}
```
