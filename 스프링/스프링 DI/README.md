# 스프링 DI

## 의존이란?

DI는 'Dependency Injection'의 약자로 우리말로는 '의존 주입'이라고 번역한다. 여기서 의존은 **객체간의 의존** 을 의미한다. 

한클래스가 다른클래스의 메서드를 실행할 때 이를 '의존'한다고 표현한다. 

> 의존은 변경에 의해 영향을 받는 관계를 의미한다. 예를들어 MemberDao insert() 메서드의 이름을 insertMember()로 변경하면 이 메서드를 사용하는 MemberregisterService 클래스의 소스코드도 함께 변경된다. 이렇게 변경에 따른 영향이 전파되는 관계를 "의존"한다고 표현한다.



### 의존대상 구현 - 의존 대상 객체를 직접 생성

~~~java
public class MemberRegisterService{
  //의존 객체를 직접생성
  private MemberDao memberdao = new MemberDao();
  ...
}
~~~

MemberRegisterService 클래스에서 의존하는 MemberDao 객체를 직접 생성하기 때문에 MemberRegisterService 객체를 생성하는 순간에 MemberDao 객체도 함께 생성된다.

~~~java
//의존하는 MemberDao의 객체도 함께 생성
MemberRegisterService svc = new MemberRegisterService();
~~~

클래스 내부에서 직접 의존 객체를 생성하는 것이 쉽긴 하지만 유지보수 관점에서 문제점을 유발할 수 있다.

그래서 사용하는 다른 방법은 **DI** 와 서비스 로케이터 이다.  여기서 스프링과 관련된 방법은 DI이다.



## DI를 통한 의존 처리

DI(Dependency Injection, 의존 주입)은 의존하는 객체를 직접 생성하는 대신 의존 객체를 전달 받는 방식을 사용한다. 

~~~java
package spring;

import java.time.LocalDateTime;

public class MemberRegisterService {
	private MemberDao memberDao;

	public MemberRegisterService(MemberDao memberDao) {
		this.memberDao = memberDao;
	}

	public Long regist(RegisterRequest req) {
		Member member = memberDao.selectByEmail(req.getEmail());
		if (member != null) {
			throw new DuplicateMemberException("dup email " + req.getEmail());
		}
		Member newMember = new Member(
				req.getEmail(), req.getPassword(), req.getName(), 
				LocalDateTime.now());
		memberDao.insert(newMember);
		return newMember.getId();
	}
}
~~~



~~~java
public MemberRegisterService(MemberDao memberDao) {
		this.memberDao = memberDao;
	}
~~~

이부분을 보면 알수 있듯이 생성자를 통해 의존 객체를 전달받는다. 즉, 생성자를 통해 MemberRegisterService가 의존하고 있는 MemberDao 객체를 주입(injection) 받은 것이다. 

~~~java
MemberDao dao = new MemberDao();
// 의존 객체를 생성자를 통해 주입한다.
MemberRegisterService svc = new MemberRegisterService(dao);
~~~



코드도 길어지고 그러는데 왜 DI를 하는 것인가?

 -> 의존 객체 변경이 유연해진다.









### Reference 

* 초보 웹 개발자를 위한 스프링 5 프로그래밍 입문 - 최범균 저


