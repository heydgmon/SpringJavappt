# Lombok이란?
- Java 의 라이브러리로 반복되는 메소드를 Annotation 기반으로 코드를 자동으로 완성해주는 라이브러리
- Lombok 을 이용해서 작성한 코드는 컴파일 과정에서 Annotation 을 이용해서 코드를 생성하고 이런 결과물이 .class 에 담기게 된다.
- 개인 Toy 프로젝트가 아닌 실무 프로젝트에서는 가급적 @Getter, @Setter, @ToString 만 사용하고 그 외의 것들 사용은 자제하거나 보수적으로 사용한다.

# Lombok의 장단점
1.장점
- Getter, Setter, ToString 등과 같은 다양한 코드를 자동 완성을 통한 생산성 향상
- 반복되는 코드 다이어트를 통한 가독성 및 유지보수성 향상

2.단점
- 만약 Intelli J에서 개발 시에는 모든 팀원이 Lombok 플러그인을 설치하여야만 한다.(최근에는 Intelli j 기본 플러그인으로 제공)
- 무분별한 어노테이션을 사용하면, 순환 참조 또는 무한 재귀 호출로 인해 StackOverFlow 가 발생할 수 있다.

# Getter와 Setter 활용
```
public class Member {
    private Long id;
    private String memberId;
    
	public Long getId() {
		return id;
	}
	public void setId(Long id) {
		this.id = id;
	}
	public String getMemberId() {
		return memberId;
	}
	public void setMemberId(String memberId) {
		this.memberId = memberId;
	}
 ```
```  
@Getter
@Setter
public class Member {
    private Long id;
    private String memberId;
}
```
