# 리팩토링

1)리팩토링의 정의 : 소프트웨어의 겉보기 동작은 그대로 유지한 채, 코드를 이해하고 수정하기 쉽도록 내부 구조를 변경하는 기법

# 리팩토링의 기법

1)Extract Method : 코드 덩어리를 별도의 코드로 분리

그룹으로 묶을 수 있는 코드가 있다면 적절한 메소드를 만들어서 해당 코드를 메소드 안으로 이동

![image](https://github.com/heydgmon/rrrr/assets/40292371/0fb58da7-4614-456d-9d16-a8988f6df2b3)


2)Inline Method : 위의 반대 개념

메소드 호출 부분이 메소드 자체보다 더 자세할 때 메소드 호출을 메소드 내용으로 바꾸고 메소드 삭제

![image](https://github.com/heydgmon/rrrr/assets/40292371/59a3ba9f-e32b-4ef7-a1a1-24f3d151c765)
