---
layout: post
title: "@Entity 코드에서 Rombok 어노테이션 이용시 주의 사항"
categories: [ etc ]
---

### 권장되지 않는 방식
``` java
@Data
public class Event {
    ... 
}
```
@Data 를 이용하여 equals, hashCode, toString 메소드를 자동 생성 했을 경우, 
코드 작성시 순환참조 발생 가능성이 매우 높아진다.
(순환 참조로 인한 스택 overflow 발생)
따라서 @Data 애노테이션을 사용하는 대신에 아래와 같은 코드로 변경하는 것이 좋다.



### 순환참조 방지를 위해 일반적인 룸복 사용 방식
``` java
@Builder @AllArgsConstructor @NoArgsConstructor
@Getter @Setter @EqualsAndHashCode(of="id")
public class Event {
    ... 
}
```

