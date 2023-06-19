# 문자열 자료형 클래스 - String, StringBuffer, StringBuilder

1. String : 불변 자료형

   한번 할당된 공간이 변하지 않음

   인스턴스 생성 시 생성자의 매개변수로 입력받는 문자열은 이 value 라는 인스턴스 변수에 문자형 배열로 저장됨(final로 변경 불가)
![123456](https://github.com/heydgmon/0619/assets/40292371/9ce67b80-07d4-42ca-b90c-1d134f1de3b9)

메모리에 "hello", "hello world"가 별도로 올라가게 되고 "hello"는 자바의 가비지 컬렉터(GC)가 제거해줌
![ppp11](https://github.com/heydgmon/0619/assets/40292371/04107a4f-11d5-45e8-bbf8-827c9b6fb8f0)

