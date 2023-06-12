# 쓰레드란?
하나의 프로세스(동작 중인 프로그램) 내에서 여러 개의 실행 흐름(단일, 동시적, 병렬적)을 두어 작업을 효율적으로 처리하기 위한 모델

```
public class Sample extends Thread {
    int seq;

    public Sample(int seq) {
        this.seq = seq;
    }

    public void run() {
        System.out.println(this.seq + " thread start.");  // 쓰레드 시작
        try {
            Thread.sleep(1000);  // 1초 대기한다.
        } catch (Exception e) {
        }
        System.out.println(this.seq + " thread end.");  // 쓰레드 종료 
    }

    public static void main(String[] args) {
        for (int i = 0; i < 10; i++) {  // 총 10개의 쓰레드를 생성하여 실행한다.
            Thread t = new Sample(i);
            t.start();
        }
        System.out.println("main end.");  // main 메서드 종료
    }
}
```

