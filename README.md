# 프록시 패턴
![proxy uml](https://user-images.githubusercontent.com/40292371/235812878-6c849bbc-f8ad-4506-b224-8337d7c4f203.png)

프록시 패턴이란? 프록시 패턴은 어떤 객체에 대한 접근을 제어하는 용도로 대리인에 해당하는 객체를 제공하는 패턴


Client : 고객


Subject : 결제


Proxy : 체크카드


RealSubject : 1)체크카드에 연관된 은행 계좌, 2)현금 등등


1)고객이 매장에 방문해서 상품을 체크카드로 결제를 하게 되면, 체크카드에 연관된 계좌에 돈이 빠져나감


체크카드는 결제를 대행해주는 Proxy 역할을 하고, 은행계좌는 외부로부터 숨겨 민감정보를 보호할 수 있음

2)고객이 매장에 방문해서 상품을 결제하려고 하는데 현금이 모자라는 경우 체크카드를 대신 사용할 수 있음

# 예시코드2)

결제 - payment interface

```
public interface Payment{
    void pay(int amount);
}
```

매장 - 이 interface를 사용하는 client쪽 code

```
public class Store{
    
    Payment payment;
    
    public Store(Payment payment){
        this.payment = payment;
    }
    
    public void buySomething(){
        payment.pay(100);
    }
}
```

현금결제

```
public class Cash implements Payment{
    public void pay(int amount){
      System.outprintln(amount+"현금 결제");
    }    
}
```

카드결제

```
public class CreditCard implements Payment{
//Credit card가 문제가 있으면 cash로 fall back

     Payment cash = new Cash();
   
     public void pay(int amount){
         if(amount>100){
           System.out.println(amount + "신용 카드")
         }else{       
         cash.pay(amount);
         }
     }
}
```
# 강의내용(AOP)

공통 관심사항과 핵심 관심사항

1)핵심 관심사항 = 회원 가입, 회원 조회와 같은 비즈니스 로직

2)공통 관심 사항 = 회원 가입이나 회원 조회의 기능을 실행하는데 걸리는 시간을 측정


```
@Transactional
public class MemberService {
    private final MemberRepository memberRepository;

    public  MemberService(MemberRepository memberRepository){
        this.memberRepository = memberRepository;
    }

    /**
     * 회원가입
     */
    public Long join(Member member){

        long start = System.currentTimeMillis();

        try {
            validateDuplicateMember(member);
            memberRepository.save(member);
            return member.getId();
        } finally{
            long finish = System.currentTimeMillis();
            long timeMs = finish - start;
            System.out.println("join " + timeMs + "ms");
        }
    }

    /**
     * 전체 회원 조회
     */
    public List<Member> findMembers(){
        
        long start = System.currentTimeMillis();
        
        try {
            return memberRepository.findAll();
        } finally {
            long finish = System.currentTimeMillis();
            long timeMs = finish - start;
            System.out.println(timeMs);
        }
    }
}

```
위 코드의 경우 공통 관심 사항과 핵심 관심사항이 분리가 안되어서 유지보수에 어려움이 있음.

예를 들어 start와 finish 변수의 System.currentTimeMillis() -> System.nanoTime()로 변경 (밀리초를 나노초로 변경) 하라는 요구 사항이 있는 경우

해당 파일을 찾아서 일일이 변경해야하는 불편함이 존재 -> AOP의 필요성

AOP를 적용하는 경우 아래와 같이 구조가 변경되는데(그림 삽입하기), 스프링 컨테이너는 프록시를 자동으로 
