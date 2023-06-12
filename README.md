# 쓰레드란?
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

