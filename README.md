# 문자열 자료형 클래스 - String, StringBuffer, StringBuilder

1. String : 불변 자료형
한번 할당된 공간이 변하지 않음

 

실제로 String 객체의 내부 구성 요소를 보면 다음과 같이 되어 있다.

인스턴스 생성 시 생성자의 매개변수로 입력받는 문자열은 이 value 라는 인스턴스 변수에 문자형 배열로 저장되게 된다. 이 value 라는 변수는 상수(final)형이니 값을 바꾸지 못하는 것이다.
