# Thread란?
하나의 프로세스(동작 중인 프로그램) 내에서 여러 개의 실행 흐름(단일, 동시적, 병렬적)을 두어 작업을 효율적으로 처리하기 위한 모델

```
public class Sample extends Thread { //Thread 클래스를 상속하는 Sample 클래스
    int num;
    public Sample(int num) {
        this.num = num;
    }

    public void run() {
        System.out.println(this.num + " thread start.");  // 쓰레드 시작
        System.out.println(this.num + " thread end.");  // 쓰레드 종료 
    }

    public static void main(String[] args) {
        for (int i = 0; i < 5; i++) {  // 총 5개의 쓰레드를 생성하여 실행한다.
            Thread t = new Sample(i);
            t.start(); // Thread 클래스를 extends 했기때문에 start 메서드 실행시 run 메서드가 수행된다.
        }
    }
}
```
실행결과

![쓰레드](https://github.com/heydgmon/0612/assets/40292371/ab7d6211-9052-4486-8eb6-04d3c9b04cfb)

* 쓰레드를 사용하면 동시에 여러개의 코드를 수행할 수 있으므로 동시에 엄청난 양의 요청이 들어올 경우 많은 양도 한번에 처리할 수 있다

# Spring에서의 Thread Pool 이해
