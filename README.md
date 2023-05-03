# 프록시 패턴
![proxy uml](https://user-images.githubusercontent.com/40292371/235812878-6c849bbc-f8ad-4506-b224-8337d7c4f203.png)

프록시 패턴이란? 프록시 패턴은 어떤 객체에 대한 접근을 제어하는 용도로 대리인에 해당하는 객체를 제공하는 패턴


Client : 고객


Subject : 결제


Proxy : 체크카드


RealSubject : 1)체크카드에 연관된 은행 계좌, 2)현금 등등


1)고객이 매장에 방문해서 상품을 체크카드로 결제를 하게 되면, 체크카드에 연관된 계좌에 돈이 빠져나감


체크카드는 결제를 대행해주는 Proxy 역할을 하고, 은행계좌는 외부로부터 숨겨 민감정보를 보호할 수 있음

2)고객이 매장에 방문해서 상품을 결제하려고 하는데 현금이 없는 경우 체크카드를 대신 사용할 수 있음

#코드

'''
1.public interface Payment{

    void pay(int amount);
}
이 interface를 사용하는 client쪽 code가 있다고 가정
2.public class Store{
    
    Payment payment;
    
    public Store(Payment payment){
        this.payment = payment;
    }
    
    public void buySomething(){
        payment.pay(amount:100);
    }
}

3.public class Cash implements Payment{

    public void pay(int amount){
      System.outprintln(amount+"현금 결제");
    }
    
}
여기까지 하면 cash만 구현된거

4,public class CreditCard implements Payment{
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
'''
 
