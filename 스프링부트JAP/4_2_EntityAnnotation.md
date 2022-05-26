### @Entity 
- 테이블과의 매핑
- @Entity가 붙은 클래스는 JPA 가 관리하는 것으로 , 엔티티라고 불림
- @Id 는 테이블의 primary key 와 같은 의미를 가짐

### @Table 
- @name TABLE 의 이름을 정할 수 있다. 적어주지 않는 경우 Entity 클래스의 이름 그대로 CamelCase 를 유지한
  채 테이블이 생성되기때문에 테이블 이름을 명시적으로 작성하는 것이 관례
- 데이터베이스상에서 보편적으로 사용되는 명명법은 UnderScore가 원칙이긴함.
- 
### @Column 
- 테이블컬럼의 이름이나 제약조건을 걸 수 있다. ( 대표적으로 길이 ) 

### @GeneratedValue 
- mysql 의 AutoIncreament 와 같이 자동으로 값을 증가시킨다.
- 대량의 요청이 유입 되더라도 deadlock 이 발생 되지 않을 만큼 키값이 빨리 생성되는 특징이있음

### @Enumerated
- java의 enum 과 같음
- 속성으로는 EnumType.ORDINAL , EnumType.STRING 이 있음 
- ORDINAL 은 0,1 로 값이 저장 STRING 은 enum 클레스의 문자열 자체가 값으로 사용됨

### @OneToOne
- 1:1 의 관계
  
### @OnetoMany
- 1:N의 관계 

### @ManyToMany
- N:M의 관계

### @mappedBy
- 양방향 관계 설정시 관계의 주체가 되는 쪽에서 정의

