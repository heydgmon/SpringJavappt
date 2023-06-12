# Spring의 동시 요청 처리 방법
->Spring은 어떻게 동시에 수많은 요청을 처리할까?

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

# Thread 사용 시 장단점
장점 : 쓰레드를 사용하면 동시에 여러개의 코드를 수행할 수 있으므로 동시에 엄청난 양의 요청이 들어올 경우 많은 양도 한번에 처리할 수 있다
단점 : 쓰레드를 지나치게 많이 생성하면 리소스가 빠르게 고갈될 수 있다 + CPU 오버헤드가 걸릴 수 있다

# Thread Pool란?
![cas](https://github.com/heydgmon/0612/assets/40292371/5bedd74f-d97a-4cfa-80f2-59c9014a1de4)

Thread Pool은 일정량의 쓰레드를 미리 만들어두고 Task Queue 를 이용해 Task 를 처리하는 패턴

특징
* 쓰레드를 미리 만들어두고 사용하기 때문에 새로운 쓰레드를 생성하는 비용을 줄일 수 있고,
* 사용할 쓰레드의 개수를 제한하기 때문에 CPU 오버헤드를 방지할 수 있다.
* 즉, 스레드 풀을 사용하면 여러 개의 작업을 동시에 안정적으로 처리할 수 있다.


# Spring에서의 Thread Pool 
스프링 부트 프로젝트를 생성할 시 스프링 부트에서는 내장 Servelt Container인 톰캣(tomcat)이 자동적으로 설정되고

Spring 에서 클라이언트의 요청은 Tomcat(Servlet Container)이 처리

# ThreadPoolExecutor
 스프링 부트에서 멀티 쓰레드(Multi thread)를 관리하기 위해서 ThreadPoolExecutor를 사용
 
Spring Boot가 실행되면 내부적으로 ThreadPoolExecutor 구현체를 생성해서 내장 톰캣이 사용할 쓰레드 풀을 생성하는 구조
 

application.yml에 아래와 같이 쓰레드 풀 프로퍼티를 추가할 수 있음(아래는 스프링 부트 default 설정)
```
server:
  tomcat:
    threads:
      max: 200  //max - 쓰레드의 최대 개수
      min-spare: 10 //min-spare - 활성화 상태로 유지할 최소 쓰레드의 개수
    accept-count: 100 //accept-count - 모든 스레드가 사용 중일때 들어오는 연결 요청 큐의 최대 길이
  port: 8080
  ```


