# 문자열 자료형 클래스 - String, StringBuffer, StringBuilder

# String : 불변 자료형, Thread-safe

 한번 할당된 공간이 변하지 않음

 인스턴스 생성 시 생성자의 매개변수로 입력받는 문자열은 이 value 라는 인스턴스 변수에 문자형 배열로 저장됨(final로 변경 불가)
 
 
![123456](https://github.com/heydgmon/0619/assets/40292371/9ce67b80-07d4-42ca-b90c-1d134f1de3b9)

![ppp11](https://github.com/heydgmon/0619/assets/40292371/04107a4f-11d5-45e8-bbf8-827c9b6fb8f0)

  메모리에 "hello", "hello world"가 별도의 객체로 올라가게 되고 "hello"는 자바의 가비지 컬렉터(GC)가 제거해줌

![rrr111](https://github.com/heydgmon/0619/assets/40292371/63f48463-9ab1-4220-bdeb-41fa9287c957)

# StringBuffer : 가변 자료형, Thread-safe

final 키워드가 없어 변경 가능


![qq1](https://github.com/heydgmon/0619/assets/40292371/d7d2134e-bdd0-4574-9deb-1d0048ff9567) 


![qq11](https://github.com/heydgmon/0619/assets/40292371/dd757e35-c561-48f5-8f86-e925cea1c34f)

동일 객체내에서 문자열 크기 변경 가능

![rrr11](https://github.com/heydgmon/0619/assets/40292371/fcb58ac7-f721-41fc-9267-cf5a10385304)


String은 불변적인 특징 때문에 값을 업데이트하면, 매 연산 시마다 새로운 문자열을 가진 String 인스턴스가 생성되어 메모리공간을 차지하므로 연산 속도가 낮음


String buffer는 가변적인 특징 때문에 값을 업데이트할 시 별도의 인스턴스 생성 없이 연산이 이루어지므로 연산 속도가 빠름 

# StringBuilder : 가변 자료형, 단일 쓰레드
StringBuilder는 StringBuffer와 같이 크기가 유연하게 변하는 가변적인 특성을 가지고 있으며, 제공하는 메서드도 똑같고 사용하는 방법도 동일하나
Thread safe 여부에서만 차이가 있다.




# String vs StringBuilder vs StringBuffer
1.String 을 사용해야 할 때 :
문자열 연산이 적고 변하지 않는 문자열을 자주 사용할 경우
멀티쓰레드 환경일 경우 

2.StringBuilder 를 사용 해야 할 때 :
문자열의 추가, 수정, 삭제 등이 빈번히 발생하는 경우
단일 쓰레드이거나 동기화를 고려하지 않아도 되는 경우
속도면에선 StringBuffer 보다 성능이 좋다.

3.StringBuffer 를 사용해야 할 때 :
문자열의 추가, 수정, 삭제 등이 빈번히 발생하는 경우
멀티쓰레드 환경일 경우 
