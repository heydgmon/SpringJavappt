1.

트랜잭션이란? 완전히 성공하거나 완전히 실패하는 일련의 논리적 작업단위, 둘 중 하나라도 실패 시 전체 프로세스는 실패 

트랜잭션 단위(ex)은행 계좌이체 ): A의 계좌에서 출금하는 금액과 B의 계좌에서 입금하는 금액

트랜잭션에는 데이터를 최종적으로 데이터베이스에 반영하는 COMMIT과 실패했을때 원 상태로 다시 되돌아가는 ROLLBACK이 있다.

-----------------------------------------------------------------------------------------------------------------------

public void buy() {

  buyer.send();		
  //구매자 출금
  seller.receive(); 
  //판매자 입금 

}

-----------------------------------------------------------------------------------------------------------------------


만약 send() 까지 실행이 되고 receive() 메소드는 실행이 되지 않을 경우 문제가 발생할 수 있음

이 경우 try-catch문을 통해 아래와 같이 구현할 수도 있지만


-----------------------------------------------------------------------------------------------------------------------
public void buy() {

  DefaultTransactionDefinition def = new DefaultTransactionDefinition();
  TransactionStatus status = transactionManager.getTransaction(def);

  try {
      buyer.send();			
      seller.receive();
      
      transactionManager.commit(status);

  } catch(Exception e) {

      transactionManager.rollback(status);

  } 
}

-----------------------------------------------------------------------------------------------------------------------


쿼리를 사용하는 메소드에 매번 중복되는 코드를 작성해 주어야 하는 불편함 존재

 @Transactional 어노테이션만 붙여주면 아래와 같이 간결하게 표현 가능

@Transactional
public void buy() {

  buyer.send();			
  seller.receive();

}


-----------------------------------------------------------------------------------------------------------------------

2.OOP와 AOP

https://velog.io/@geesuee/Spring-AOPAspect-Oriented-Programming%EC%99%80-%ED%94%84%EB%A1%9D%EC%8B%9C


위와 같이 프로그램을 짜면,
로깅, 보안, 트랜잭션과 같은 공통된 로직이 매 비즈니스 로직마다 반복되어 작성된다. 
반복된 코드 작성을 피하고, 유지 보수 및 확장을 용이하게 하려면?

AOP를 적용하여 비즈니스 로직과 공통 로직을 분리하고, 매핑해주어야 한다. 


3.@Transactional 사용 주의점

@Transactional은 Proxy 형태로 동작한다.

1) private은 @Transactional이 적용되지 않는다.

@Transactional 
private void createUser(){
	
}
@Transactional은 Proxy 형태로 동작하기 때문에 외부에서 접근이 가능한 메서드만 설정할 수 있다.

2) 같은 클래스 내 여러 @Transactional method 호출
@Transactional
public void createUserList(){
    for (int i = 0; i < 10; i++) {
        createUser(i);
    }
}

@Transactional
public User createUser(int index){
    User user = User.builder()
            .name("testname::"+index)
            .email("testemail::"+index)
            .build();
    
    userRepository.save(user);
    return user;
}
위 코드는 실행하면 10번의 createUser가 실행되지만 User는 생성되지 않는다. 그 이유는 @Transactional이 Proxy 형태로 동작하기 때문이다.



