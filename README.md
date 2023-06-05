# Lombok이란?
- Java 의 라이브러리로 반복되는 메소드를 Annotation 기반으로 코드를 자동으로 완성해주는 라이브러리
- Lombok 을 이용해서 작성한 코드는 컴파일 과정에서 Annotation 을 이용해서 코드를 생성하고 이런 결과물이 .class 에 담기게 된다.
- 개인 Toy 프로젝트가 아닌 실무 프로젝트에서는 가급적 @Getter, @Setter, @ToString 만 사용하고 그 외의 것들 사용은 자제하거나 보수적으로 사용한다.

# Lombok의 장단점
1.장점
- Getter, Setter, ToString 등과 같은 다양한 코드를 자동 완성을 통한 생산성 향상
- 반복되는 코드 다이어트를 통한 가독성 및 유지보수성 향상

2.단점
- 무분별하게 lombok을 사용하면, 순환 참조 또는 무한 재귀 호출로 인해 StackOverFlow 가 발생할 수 있다.

# Getter와 Setter 활용
```
public class Member {
    private Long id;
    private String memberId;
    
	public Long getId() {
		return id;
	}
	public void setId(Long id) {
		this.id = id;
	}
	public String getMemberId() {
		return memberId;
	}
	public void setMemberId(String memberId) {
		this.memberId = memberId;
	}
 ```
```  
@Getter
@Setter
public class Member {
    private Long id;
    private String memberId;
}
```

# ToString 활용
```
public class Member {
    private Long Id;
    private String memberId;

public String toString(){
 return "Member(Id=" + this.Id +",memberId = "this.memberId +")";
 }
}

```

```
@ToString
public class Member {
    private Long Id;
    private String memberId;
}
```

# @AllArgsConstructor, @RequiredArgsConstructor 사용금지

```
@AllArgsConstructor
public static class Order {
    private long cancelPrice;
    private long orderPrice;
}
 
// 취소금액 5,000원, 주문금액 10,000원
Order order = new Order(5000L, 10000L); 
```
cancelPrice, orderPrice 순서로 인자를 받는 생성자가 만들어진다. 
개발자가 cancelPrice가 orderPrice보다 위에 있는것이 마음에 안들어서 순서를 다음과 같이 바꾼다고 하면

```
@AllArgsConstructor
public static class Order {
    private long orderPrice;
    private long cancelPrice;
}
```
lombok이 개발자도 인식하지 못하는 사이에 생성자의 파라미터 순서를 필드 선언 순서에 맞춰 orderPrice,cancelPrice로 바꿔버린다. 게다가 이 두 필드는 동일한 Type 이라서 어떠한 오류도 발생하지 않는다.
위의 생성자를 호출하는 코드는 아무런 에러없이 잘 작동하는 듯 보이지만 실제로 입력된 값은 바뀌어 들어가게 된다.

```
// 주문금액 5,000원, 취소금액 10,000원. 취소금액이 주문금액보다 많아짐
Order order = new Order(5000L, 10000L); // 인자값의 순서 변경 없음
```
이 문제는 @AllArgsConstructor와 @RequiredArgsConstructor에 둘 다 존재하며, 이에 따라 이 두 lombok 애노테이션은 사용을 금지하는 것이 좋다.

대신, 생성자를 직접 만들고 필요할 경우에는 직접 만든 생성자에 @Builder 애노테이션을 붙이는 것을 권장한다. 파라미터 순서가 아닌 이름으로 값을 설정하기 때문에 리팩토링에 유연하게 대응할 수 있다.
```
public static class Order {
    private long cancelPrice;
    private long orderPrice;
 
    @Builder
    private Order(long cancelPrice, long orderPrice) {
        this.cancelPrice = cancelPrice;
        this.orderPrice = orderPrice;
    }
}
 ```
 ```
// 필드 순서를 변경해도 문제 없음.
Order order = Order.builder().cancelPrice(5000L).orderPrice(10000L).build();
System.out.println(order);
```

