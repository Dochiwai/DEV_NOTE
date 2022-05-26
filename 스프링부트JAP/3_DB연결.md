### properties.yml 정보
```
spring:
  datasource:
    url: jdbc:h2:tcp://localhost/~/jpashop;
    username: sa
    password:
    driver-class-name: org.h2.Driver

  jpa:
    hibernate:
      ddl-auto: create
    properties:
      hibernate:
        show_sql: true
        format_sql: true
        
logging:
  level: 
    org.hibernate.SQL: debug
    #쿼리에 파라미터 값까지 볼 수 있다.
    org.hibernate.type: trace
```

```
dependencies {
  
  ...
	#쿼리에 들어가는 파라미터 값을 볼 수 있음
  implementation 'com.github.gavlyukovskiy:p6spy-spring-boot-starter:1.5.6'
  
  ...
}
```

### 멤버 Entity

```
@Entity
@Getter @Setter
public class Member {

    @Id @GeneratedValue
    private long id;
    private String username;

}
```

### 멤버 Repository
```
@Repository
public class MemberRepository {

    @PersistenceContext
    private EntityManager em;

    public Long save(Member member){
        em.persist(member);
        return member.getId();
    }

    public Member find(Long id){
        return em.find(Member.class,id);
    }

}
```

### 테스트 코드

```
import org.assertj.core.api.Assertions;
import org.junit.jupiter.api.Test;
import org.junit.runner.RunWith;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.boot.test.context.SpringBootTest;
import org.springframework.test.context.junit4.SpringRunner;
import org.springframework.transaction.annotation.Transactional;


import static org.junit.jupiter.api.Assertions.*;

@RunWith(SpringRunner.class)
@SpringBootTest
@Transactional // 엔티티는 매니저를 통한 모든 데이터 변경은 트랜잭션 안에서 해야된다.
//@Rollback(false) 데이터 초기화를 막음
class MemberRepositoryTest {

    @Autowired MemberRepository memberRepository;

    @Test
    public void testMember() throws Exception{
        Member member = new Member();
        member.setUsername("memberA");

        Long saveId = memberRepository.save(member);
        Member findMember = memberRepository.find(saveId);

        Assertions.assertThat(findMember.getId()).isEqualTo(member.getId());
        Assertions.assertThat(findMember.getUsername()).isEqualTo(member.getUsername());


    }

}
```


