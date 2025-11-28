# QueryDSL 핵심 정리 및 실무 활용 가이드

## 1. QueryDSL이란?

**QueryDSL**은 하이버네이트 쿼리 언어(HQL) 또는 JPQL(Java Persistence Query Language)**을 문자열이 아닌 자바 코드로 작성할 수 있도록 도와주는 오픈소스 빌더 프레임워크입니다.

### 왜 사용하는가?

- 기본적인 CRUD는 `Spring Data JPA`로 해결 가능하지만, 복잡한 조회 쿼리나 동적 쿼리를 구현하기에는 한계가 있습니다.
- 문자열(String) 형태의 JPQL은 런타임 시점에 오류가 발견되지만, QueryDSL은 코드 기반이므로 컴파일 시점에 문법 오류를 잡을 수 있습니다.

---

## 2. 주요 특징 및 장점

1. 타입 안전성 (Type Safety)
    - `QEntity`라는 전용 클래스를 사용하여 코드로 작성하므로, 오타나 존재하지 않는 필드 참조 시 컴파일 에러가 발생하여 안전합니다.
2. 동적 쿼리 해결 (Dynamic Query)
    - `BooleanExpression`을 활용하여 조건문을 메서드 단위로 분리하고 조합할 수 있습니다.
    - 조건이 `null`일 경우 `Where` 절에서 자동으로 무시되므로 동적 쿼리 작성이 매우 유연합니다.
3. 가독성 및 유지보수
    - SQL과 유사한 직관적인 문법을 제공합니다.
    - 복잡한 쿼리 로직을 메서드로 분리하여 재사용할 수 있습니다.

---

## 3. 기본 문법

### 검색 조건 (Where 절)

- **비교:** `.eq()`, `.ne()`, `.gt()`, `.lt()`, `.goe()`, `.loe()`
- **범위:** `.between()`, `.in()`, `.notIn()`
- **검색:** `.like()`, `.contains()`, `.startsWith()`, `.endsWith()`
- **논리 연산:** `.and()`, `.or()`, `.not()`

### 정렬 및 조회 (OrderBy, Fetch)

- `.orderBy(e.field.desc())`: 내림차순 정렬 (`asc()`: 오름차순)
- `.nullsLast()`, `.nullsFirst()`: null 값의 정렬 순서 지정
- `.fetch()`: 리스트 반환
- `.fetchOne()`: 단건 조회 (결과 없으면 null, 둘 이상이면 예외 발생)
- `.fetchFirst()`: `.limit(1).fetchOne()`과 동일

---

## 4. 실무 활용 전략 (Best Practices)

### 1) 페이징(Paging) 성능 최적화

- `fetchResults()`와 `fetchCount()`는 QueryDSL 5.0부터 Deprecated 되었습니다.
- 따라서 Content 쿼리와 Count 쿼리를 별도로 작성하여 분리하는 것이 권장됩니다.
- 특히 Count 쿼리에서는 데이터 조회에 불필요한 `Join`을 제거하거나 최적화하여 성능을 높여야 합니다.

### 2) DTO 직접 조회 (Projections)

- 엔티티를 직접 조회하여 컨트롤러까지 넘기기보다는, 필요한 데이터만 뽑아 DTO로 반환하는 방식을 선호합니다.
- `Projections.constructor` 방식을 사용하여 생성자 기반으로 바인딩하면, 필드명 불일치 문제를 피하고 불변 객체로 활용할 수 있습니다. (단, 생성자 파라미터 순서와 타입이 일치해야 함)

### 3) BooleanExpression을 활용한 조건 모듈화

- `where` 절에 들어갈 조건을 별도의 메서드(`BooleanExpression` 반환)로 분리합니다.
- 이렇게 하면 코드 가독성이 좋아지고, `isServiceable()` 같은 비즈니스 용어의 메서드로 만들어 다른 조회 로직에서도 재사용할 수 있습니다.

### 4) N+1 문제 해결 (Fetch Join)

- 연관된 엔티티를 한 번에 가져올 때 `.fetchJoin()`을 사용합니다.
- 주의: 컬렉션(1:N) 페치 조인 시 페이징을 하면 하이버네이트가 메모리에서 페이징 처리를 하므로 장애 원인이 될 수 있습니다. (N:1 관계는 안전)

### 5) 영속성 컨텍스트 주의 (Bulk 연산)

- `update`, `delete` 같은 벌크 연산은 영속성 컨텍스트(1차 캐시)를 무시하고 DB에 바로 반영됩니다.
- 데이터 불일치를 막기 위해 벌크 연산 실행 후에는 반드시 `em.flush()`와 `em.clear()`를 호출해야 합니다.

---

## 5. 코드 예제

아래는 동적 쿼리, DTO 매핑, 서브쿼리, 조인을 활용한 예제입니다.

```java
QEntity e = QEntity.entity

List<Entity> list = queryFactory
    .selectFrom(e) //e 테이블 선택
    .where(
        e.name.eq("aaa"), //name이 aaa이면서
        e.size.gt(180) //size가 180보다 큰
    )
    .orderBy(e.createdAt.desc()) // createdAt을 기준으로 내림차순
    .fetch(); //query실행후 List 반환

```

```java
public List<MemberDto> searchMembers(String username, Integer minAge, Integer maxAge, String teamName) {
    QMember m = QMember.member; // Member 엔티티를 기반으로 자동 생성된 Q타입
    QTeam t = QTeam.team; // Team엔티티를 기반으로 자동 생성된 Q타입
    QMember sub = new QMember("sub"); // 서브쿼리용 별칭

    return queryFactory
        .select(Projections.constructor(MemberDto.class, //원하는 결과값만 프로잭션
            m.id,
            m.username,
            t.name))
        .from(m) //Member 엔티티를 기준으로 조회
        .leftJoin(m.team, t) //Member와 Team을 join(팀이 없는 회원도 포함)
        .where(
            // null 무시 패턴: 값이 없으면 조건 제외
            usernameEq(username),
            ageGoe(minAge),
            ageLoe(maxAge),
            teamNameEq(teamName),

            // 서브쿼리: 평균 나이보다 많은 회원만
            m.age.gt(
                JPAExpressions // JPA환경에서 서브쿼리 작성을 위함
                    .select(sub.age.avg())
                    .from(sub)
            )
        )
        // 최신 가입일 기준 내림차순 정렬
        .orderBy(m.createdAt.desc())
        .fetch(); //fetch말고도 fetchOne(), fetchFirst(), fetchCount()등의 값도 있음
}

// 조건 생성기 (BooleanExpression 반환, null이면 where절에서 무시됨)
이이
private BooleanExpression ageGoe(Integer minAge) {
    return minAge != null ? QMember.member.age.goe(minAge) : null;
}
private BooleanExpression ageLoe(Integer maxAge) {
    return maxAge != null ? QMember.member.age.loe(maxAge) : null;
}
private BooleanExpression teamNameEq(String teamName) {
    return (teamName != null && !teamName.isBlank()) ? QTeam.team.name.eq(teamName) : null;
}
```
