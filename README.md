# proxy
스터디
https://refactoring.guru/design-patterns/proxy

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
