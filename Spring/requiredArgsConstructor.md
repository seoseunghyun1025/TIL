## @RequiredArgsConstructor
- 클래스 내에 final 키워드가 붙은 필드들을 모아서 생성자를 만들어 줌
- final이 아니더라도 @NonNull이 붙은 필드가 있다면 생성자 파라미터에 포함

#### 사용 전
```java
@Service
public class MemberService {

    private final MemberRepository memberRepository;
    private final EmailService emailService;

    // 생성자를 직접 작성해야 함
    public MemberService(MemberRepository memberRepository, EmailService emailService) {
        this.memberRepository = memberRepository;
        this.emailService = emailService;
    }
}
```

#### 사용 후
```java
@Service
@RequiredArgsConstructor // 생성자 코드를 작성할 필요가 없음
public class MemberService {

    private final MemberRepository memberRepository;
    private final EmailService emailService;
}
```

#### 주의할 점
- 가능하면 생성자를 직접 작성하거나 지양
- 클래스에 선언된 필드의 작성 순서를 기준으로 생성자 파라미터 순서를 자동으로 결정
  - 리펙토링 과정에서 타입이 같은 필드 두 개의 순서가 바뀌면 컴파일 에러가 나지 않고 런타임 시점에 엉뚱한 객체가 주입
- 너무 쉽게 만들어지다 보니 수십 개의 빈을 주입받는 비대한 클래스가 되기 쉬움
