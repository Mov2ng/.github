# Mov2ng 프로젝트 중간 기술발표

> **발표 시간**: 15분  
> **발표 일자**: 2026.01.02(금)
> **프로젝트 기간**: 2개월 (현재 1개월 경과)

---

## 📋 목차

1. [프로젝트 개요](#1-프로젝트-개요) (1분)
2. [기술 스택 선정 이유](#2-기술-스택-선정-이유) (1분)
3. [전체 아키텍처](#3-전체-아키텍처) (1분)
4. [핵심 기능 소개](#4-핵심-기능-소개) (10분)
   - 4.1 인증/유저 시스템 (홍명주) - 2분
   - 4.2 프로필/마이페이지 (홍명주) - 2분
   - 4.3 견적 요청 시스템 (김성준/김연만) - 2분
   - 4.4 기사님 찾기 (조원정) - 2분
   - 4.5 리뷰 작성/조회 (원치준) - 2분
5. [전체적인 기술적 도전 과제](#5-전체적인-기술적-도전-과제) (1분)
6. [결과 및 회고](#6-결과-및-회고) (1분)

---

## 1. 프로젝트 개요

### 프로젝트 한 줄 요약

**Mov2ng**은 이사 서비스를 필요로 하는 사용자와 이사 기사님을 연결하는 매칭 플랫폼

### 개발 정보

- **개발 기간**: 2개월 (현재 1개월 경과)
- **인원**: 5명
- **역할 분담**:
  - A: 인증/유저, 프로필/마이페이지
  - B: 기사님 찾기 (비회원/유저)
  - C: 견적 결과 관리 (유저), 리뷰 작성/조회
  - D/E: 견적 요청, 견적 요청 관리 (기사님), 알림 기능

### 대상 사용자 & 해결하려는 문제

**문제점**:

- 이사 서비스 이용 시 신뢰할 수 있는 기사님을 찾기 어려움
- 견적 비교가 불편하고 투명하지 않음
- 기사님과 사용자 간 직접적인 소통 부재

**해결책**:

- 사용자는 여러 기사님의 견적을 한 번에 비교 가능
- 기사님은 자신의 프로필과 경력을 어필하여 고객 확보
- 리뷰 시스템을 통한 신뢰도 향상
- 실시간 알림을 통한 견적 요청 및 수락 관리

---

## 2. 기술 스택 선정 이유

### Frontend

| 기술                      | 선택 이유                                  | 대안 기술과 비교                       |
| ------------------------- | ------------------------------------------ | -------------------------------------- |
| **Next.js 16**            | SSR/SSG 지원, 파일 기반 라우팅, API Routes | React만 사용 시 라우팅/빌드 설정 복잡  |
| **TypeScript**            | 타입 안전성, IDE 자동완성, 리팩토링 안전성 | JavaScript는 런타임 에러 위험          |
| **TanStack Query**        | 서버 상태 관리, 캐싱, 자동 리프레시        | SWR 대비 더 풍부한 기능, DevTools 제공 |
| **Zustand**               | 클라이언트 상태 관리, 간단한 API           | Redux 대비 보일러플레이트 적음         |
| **React Hook Form + Zod** | 폼 검증, 성능 최적화, 타입 안전성          | Formik 대비 리렌더링 최소화            |
| **Tailwind CSS**          | 유틸리티 퍼스트, 빠른 개발 속도            | CSS-in-JS 대비 빌드 크기 최적화        |

### Backend

| 기술           | 선택 이유                                | 대안 기술과 비교                                   |
| -------------- | ---------------------------------------- | -------------------------------------------------- |
| **Express.js** | 가볍고 유연함, 미들웨어 생태계 풍부      | NestJS 대비 학습 곡선 낮음, 빠른 프로토타이핑      |
| **TypeScript** | 타입 안전성, 프론트엔드와 타입 공유 가능 | JavaScript는 런타임 에러 위험                      |
| **Prisma**     | 타입 안전한 ORM, 마이그레이션 관리 용이  | TypeORM 대비 더 나은 타입 추론, Prisma Studio 제공 |
| **PostgreSQL** | 관계형 데이터, 트랜잭션 지원, 확장성     | MongoDB 대비 복잡한 관계 모델링에 적합             |
| **JWT**        | Stateless 인증, 확장성                   | Session 대비 서버 부하 감소                        |
| **Zod**        | 런타임 검증, TypeScript 타입 자동 생성   | Joi 대비 TypeScript 통합 우수                      |
| **Winston**    | 구조화된 로깅, 다양한 전송 방식          | console.log 대비 프로덕션 환경 대응                |

### Infra & DevOps

| 기술             | 선택 이유                             | 대안 기술과 비교                        |
| ---------------- | ------------------------------------- | --------------------------------------- |
| **Vercel** (FE)  | Next.js 최적화, 자동 배포, CDN        | AWS Amplify 대비 설정 간단              |
| **EC2/RDS** (BE) | 유연한 인프라 구성, PostgreSQL 호스팅 | Docker + Kubernetes 대비 초기 설정 간단 |

### 협업 도구
<img width="728" height="801" alt="image" src="https://github.com/user-attachments/assets/838c1a0b-6976-4b20-8219-7e060cd9e1f8" />
<img width="222" height="652" alt="image" src="https://github.com/user-attachments/assets/d6999a1a-cf62-4be2-8a78-d09d0052d5fe" />


---

## 3. 전체 아키텍처

### 시스템 구성도

```
┌─────────────────────────────────────────────────────────────┐
│                    클라이언트 (Next.js)                        │
│  ┌──────────────┐  ┌──────────────┐  ┌──────────────┐       │
│  │  Components  │→ │    Hooks     │→ │   Services   │       │
│  └──────────────┘  └──────────────┘  └──────────────┘       │
│                          ↓                                  │
│                    ┌──────────────┐                         │
│                    │  API Client  │                         │
│                    └──────────────┘                         │
└─────────────────────────────────────────────────────────────┘
                          ↓ HTTP (REST API)
┌─────────────────────────────────────────────────────────────┐
│                    서버 (Express.js)                         │
│  ┌──────────────┐  ┌──────────────┐  ┌──────────────┐       │
│  │  Routes      │→ │  Middleware  │→ │ Controllers  │       │
│  └──────────────┘  └──────────────┘  └──────────────┘       │
│                          ↓                                  │
│  ┌──────────────┐  ┌──────────────┐  ┌──────────────┐       │
│  │  Services    │→ │ Repositories │→ │   Prisma     │       │
│  └──────────────┘  └──────────────┘  └──────────────┘       │
└─────────────────────────────────────────────────────────────┘
                          ↓
┌─────────────────────────────────────────────────────────────┐
│              데이터베이스 (PostgreSQL)                         │
└─────────────────────────────────────────────────────────────┘
```

### 클라이언트-서버 흐름

1. **프론트엔드**: 사용자 액션 → React Hook Form 검증 → Custom Hook → Service → API Client
2. **백엔드**: Route → Middleware (검증/인증) → Controller → Service → Repository → Prisma
3. **응답**: Prisma → Repository → Service → Controller → ApiResponse → Express → API Client → React Query

### 배포 구조

- **프론트엔드**: Vercel (자동 배포, CDN)
- **백엔드**: 운영 - AWS EC2 (Express 서버) | 개발 - Render
- **데이터베이스**: AWS RDS (PostgreSQL) | 개발 - Render

---

## 4. 핵심 기능 소개

### 4.1 인증/유저 시스템 (A) - 2분

<img width="735" height="804" alt="image" src="https://github.com/user-attachments/assets/801c4be0-c945-4639-a657-b5c71b11e943" />


#### 기능 설명

- 회원가입: USER/DRIVER 역할 구분, 이메일 중복 체크
- 로그인: JWT 기반 인증, Access Token (2시간) + Refresh Token (7일, HTTP-only 쿠키)
- 로그아웃: 토큰 무효화
- 내 정보 조회: `/auth/me` API로 현재 로그인한 사용자 정보 조회
- 자동 토큰 갱신: API 요청 중 Access Token 만료 시 자동으로 Refresh Token으로 재발급

#### 기술적 도전 과제

**1. 역할 기반 인증 설계**

- 문제: 동일 이메일로 USER/DRIVER 가입 가능해야 함
- 해결: `email + role` 조합으로 유니크 제약 조건 설계
- 코드:

```typescript
// Prisma Schema
model User {
  email String
  role  Role
  // email + role 조합으로 유니크 체크
}

// Repository
async findUserByEmailAndRole(email: string, role: Role) {
  return prisma.user.findFirst({
    where: { email, role, isDelete: false }
  });
}
```

**2. JWT 토큰 보안 강화**

- 문제: Access Token 탈취 시 보안 위험
- 해결:
  - Access Token: 짧은 수명 (2시간), localStorage 저장, 401(토큰 만료 에러) 발생 시 자동으로 재발급 (refreshToken 사용)
  - Refresh Token: 긴 수명 (7일), HTTP-only 쿠키 저장
  - Secure, SameSite 플래그로 XSS/CSRF 방지
- 코드:

```typescript
// 로그인 시 Refresh Token을 HTTP-only 쿠키에 저장
res.cookie("refreshToken", newRefreshToken, {
  httpOnly: true, // JavaScript 접근 불가 (XSS 공격 방지)
  secure: env.NODE_ENV === "production", // HTTPS에서만 전송
  sameSite: "strict", // CSRF 공격 방지
  maxAge: 1000 * 60 * 60 * 24 * 7, // 7일
});
```

**3. 비밀번호 보안**

- 문제: 평문 비밀번호 저장 위험
- 해결: Argon2 해싱 알고리즘 사용
  - Argon2 선택 이유:
    - CPU 알고리즘(CPU 연산 위주, 메모리 접근 적음) 사용하는 bcrypt와 달리 메모리 하드 알고리즘(해싱 시 대량의 메모리 접근 필수, GPU 병렬화 효과 제한) 사용
    - GPU/ASIC 공격(그래픽카드(GPU, 수천 개 코어)나 전용 칩(ASIC)으로 병렬 무차별 대입 공격)에 더 강함(큰 메모리 요구, 예측 불가능한 접근, 순차 의존성)
    - 최신 표준 (2015년 Password Hashing Competition 우승)
- 코드:

```typescript
// 비밀번호 해싱
const hashedPassword = await argon2.hash(password, {
  type: argon2.argon2id, // 메모리 기반 + 사이드채널 공격 방어
  memoryCost: 19456, // 해싱에 사용할 메모리 용량: 약 19MB (기존 64MB보단 낮으나, 응답시간 고려해 짧게)
  timeCost: 2, // 해싱 반복 횟수 (무차별 대입 공격 방어 적정선 2~3회)
  parallelism: 1, // 해싱 연산에 사용될 병렬 스레드 수: 단일 스레드 (memoryCost x parallelism 서버 CPU 코어와 부하 고려)
});
```

#### 성능 및 품질 개선

- 클라이언트/서버 양쪽 Zod 검증으로 불필요한 요청 차단
- `asyncWrapper`로 비동기 에러 자동 처리
- 표준화된 `ApiError`/`ApiResponse`로 일관된 에러 처리
- 프론트엔드에서 API 요청 시 401 발생하면 자동으로 Refresh Token으로 Access Token 재발급 후 재시도
- 로그인 성공 시 프로필 완성 여부 확인하여 미완성 시 프로필 설정 페이지로 리디렉션

#### 남은 한 달 계획

- [ ] Sliding Session 구현: Refresh Token 사용 시 새로운 Refresh Token도 발급하여 만료 시간 연장
- [ ] 소셜 로그인 (Kakao, Naver, Google) 추가

---

### 4.2 프로필/마이페이지 (홍명주) - 2분

#### 기능 설명

- 프로필 등록: USER는 서비스 카테고리/지역, DRIVER는 추가로 닉네임/경력/소개 입력
- 프로필 이미지: 랜덤 아바타 이미지 경로로 등록
- 프로필 조회: 마이페이지에서 본인 프로필 확인
- 프로필 수정: 등록된 프로필 정보 수정
- 로그인 시 프로필 완성 여부 확인하여 미완성 시 프로필 설정 페이지로 자동 리디렉션

#### 기술적 도전 과제

**1. 역할별 동적 스키마 검증**

- 문제: USER와 DRIVER가 입력해야 하는 필드가 다름
- 해결: Zod 스키마를 동적으로 생성
- 코드:

```typescript
export const profileSchema = (role?: "USER" | "DRIVER") => {
  const isDriver = role === "DRIVER";
  const baseSchema = z.object({
    serviceCategories: z.array(z.string()).min(1),
    region: z.array(z.string()).min(1),
  });

  if (isDriver) {
    return baseSchema.extend({
      nickname: z.string().min(1).max(50), // DRIVER만 필수
    });
  }
  return baseSchema;
};
```

**2. 트랜잭션으로 원자성 보장**

- 문제: Service, Region, Driver 테이블에 동시에 데이터 삽입 필요
- 해결: Prisma 트랜잭션 사용
- 코드:

```typescript
return await prisma.$transaction(async (tx) => {
  // Service 생성
  await Promise.all(
    data.serviceCategories.map((category) =>
      tx.service.create({ data: { user_id: userId, category } })
    )
  );
  // Region 생성
  await Promise.all(
    data.region.map((region) =>
      tx.region.create({ data: { user_id: userId, region } })
    )
  );
  // Driver 프로필 생성 (DRIVER인 경우만)
  if (role === Role.DRIVER) {
    await tx.driver.create({ data: { user_id: userId, ...driverData } });
  }
});
```

**3. 프로필 이미지 처리**

- 현재: 랜덤 아바타 이미지 사용
- 향후: S3 Presigned URL 방식으로 업로드 구현 예정

#### 성능 및 품질 개선

- React Hook Form의 `defaultValues`로 수정 모드 지원
- 프로필 수정 시 기존 데이터는 Soft Delete 후 새로 생성 (데이터 이력 보존)
- 프로필 조회 시 `include`로 필요한 관계 데이터만 한 번에 조회
- 로그인 시 프로필 완성 여부 확인하여 첫 로그인 사용자는 프로필 설정 페이지로 자동 리디렉션

#### 남은 한 달 계획

- [ ] 프로필 이미지 S3 업로드 구현
- [ ] 마이페이지 기능 구현 (기사님 뿐만 아니라 회원도 마이페이지 추가 고려)
- [ ] 프로필 및 기본 정보 수정 기능 구현

---

### 4.3 견적 요청 시스템 (김성준/김연만) - 2분

#### 기능 설명

- 견적 요청 생성: 사용자가 이사 정보(출발지/도착지/날짜/서비스 타입) 입력
- 견적 요청 관리: 기사님이 받은 견적 요청 목록 조회 및 견적 제시

#### 기술적 도전 과제

**1. 견적 요청-견적 관계 모델링**

- 문제: 하나의 요청에 여러 기사님이 견적을 제시할 수 있어야 함
- 해결: Request와 Estimate를 1:N 관계로 설계
- 코드:

```typescript
// Prisma Schema
model Request {
  id          Int
  user_id     String
  moving_type Category
  moving_data DateTime
  origin      String
  destination String
  estimates   estimate[]  // 1:N 관계
}

model estimate {
  id         Int
  request_id Int
  driver_id  Int
  status     EstimateStatus  // PENDING, ACCEPTED, REJECTED
  price      Int
  request    Request @relation(...)
  driver     Driver  @relation(...)
}
```

**2. 견적 상태 관리**

- 문제: 견적 수락/거절 상태를 효율적으로 관리해야 함
- 해결: `EstimateStatus` enum으로 상태 관리, 트랜잭션으로 원자성 보장
- 코드:

```typescript
enum EstimateStatus {
  PENDING   // 대기 중
  ACCEPTED  // 수락됨
  REJECTED  // 거절됨
}

// 견적 수락 시 다른 견적들은 자동으로 REJECTED 처리
await prisma.$transaction(async (tx) => {
  // 선택한 견적을 ACCEPTED로 변경
  await tx.estimate.update({
    where: { id: acceptedEstimateId },
    data: { status: EstimateStatus.ACCEPTED },
  });
  // 같은 요청의 다른 견적들을 REJECTED로 변경
  await tx.estimate.updateMany({
    where: {
      request_id: requestId,
      id: { not: acceptedEstimateId },
    },
    data: { status: EstimateStatus.REJECTED },
  });
});
```

**3. 견적 요청 필터링 및 페이지네이션**

- 문제: 기사님이 받은 견적 요청이 많을 경우 성능 이슈
- 해결: 커서 기반 페이지네이션, 서비스 카테고리/지역 필터링
- 코드:

```typescript
async function getRequestsByDriver(
  driverId: string,
  cursor?: number,
  limit: number = 20,
  filters?: { category?: Category; region?: RegionType }
) {
  return prisma.request.findMany({
    where: {
      moving_type: filters?.category,
      // 지역 필터링 로직...
      estimates: {
        none: { driver_id: driverId }, // 아직 견적 제시하지 않은 요청만
      },
    },
    take: limit,
    skip: cursor ? 1 : 0,
    cursor: cursor ? { id: cursor } : undefined,
    orderBy: { createdAt: "desc" },
  });
}
```

#### 성능 및 품질 개선

- 견적 요청 조회 시 필요한 관계 데이터만 `include`로 조회 (N+1 문제 방지)
- 견적 수락 시 트랜잭션으로 데이터 일관성 보장
- 견적 요청 생성 시 유효성 검증 (날짜가 과거가 아닌지, 출발지/도착지가 다른지 등)

#### 남은 한 달 계획

- FE (김성준)
  - [ ] 알림 컴포넌트 구현
  - [ ] 알림 로직 구현
- BE (김연만)
  - [ ] 견적 요청 수정 기능 고려
  - [ ] 견적 요청 알림 기능 구현

---

### 4.4 기사님 찾기 (조원정) - 2분

<img width="735" height="803" alt="image" src="https://github.com/user-attachments/assets/2d546f88-4a99-422b-981d-7bed80975bc0" />
<img width="735" height="806" alt="image" src="https://github.com/user-attachments/assets/8d757ac2-faef-4186-9f72-1a9d4cb49900" />


#### 기능 설명

- 비회원/유저 모두 기사님 목록 조회 가능
- 필터링: 서비스 카테고리, 지역, 평점, 경력 등
- 정렬: 평점순, 리뷰 수순, 경력순 등
- 찜하기: 유저만 찜한 기사님 저장 가능

#### 기술적 도전 과제

**1. 각 계층의 책임이 분명하게 분리되어 있어 유지보수와 테스트가 용이**

| 계층       | 책임                       |
| ---------- | -------------------------- |
| Routes     | 라우팅, 미들웨어 적용      |
| Controller | 요청/응답 처리             |
| Service    | 비즈니스 로직, 데이터 가공 |
| Repository | 데이터베이스 접근          |

**2. 커서 기반 페이지네이션**

```jsx
cursor: cursor ? { id: cursor } : undefined,
skip: query.cursor ? 1 : 0,
```

- 무한 스크롤에 최적화된 방식
- Offset 기반보다 대량 데이터에서 성능 우수
- 실시간 데이터 변경에도 안정적

**3. 조건부 관계 조회 (Conditional Include)**

```jsx
favoriteDriver: userId
? {
where: { user_id: userId, isDelete: false },
select: { id: true },
take: 1,
}
: false,
```

- 로그인 여부에 따라 쿼리 최적화
- 불필요한 JOIN 방지
- Prisma의 조건부 include 기능 활용

**4. 선택적 인증 미들웨어**

```jsx
moverRouter.get(
  "/",
  optionalAuthMiddleware, // 로그인 안 해도 OK
  moverController.getMovers
);

moverRouter.post(
  "/:id/favorite",
  authMiddleware, // 로그인 필수
  moverController.createMoverFavorite
);
```

- 공개 API와 인증 필요 API 명확히 구분
- 로그인 시 추가 정보(isFavorite) 제공

**5. 데이터 가공 분리**

```jsx
// Repository: 순수 DB 조회
return prisma.driver.findMany({ ... });

// Service: 비즈니스 로직 + 응답 형식 변환
return drivers.map((driver) => ({
id: [driver.id](http://driver.id/),
rating: Math.round(averageRating * 10) / 10,
serviceCategories: driver.user.service.map((s) => s.category),
// ...
}));
```

- Repository는 DB 접근만 담당
- Service에서 응답 형식으로 변환
- 관심사의 분리 (SoC) 원칙 준수

**6. 캐시 활용**

```jsx
// moversDetailPage.tsx
const cachedMover = useMemo(() => {
  const queries =
    queryClient.getQueriesData <
    MoversCache >
    {
      queryKey: ["movers"],
    };
  // 캐시에서 데이터 찾기
  for (const [, data] of queries) {
    const found = data?.data?.list?.find((mover) => mover.id === idNumber);
    if (found) return found;
  }
  return null;
}, [queryClient, idNumber]);
```

- 목록에서 이미 불러온 데이터를 상세 페이지에서 재활용
- 불필요한 API 호출 감소
- 사용자 경험 향상 (빠른 페이지 전환)

#### 성능 및 품질 개선

- 페이지네이션으로 대량 데이터 조회 시 성능 최적화
- `include`로 필요한 관계 데이터만 한 번에 조회 (N+1 문제 방지)
- 인덱스 추가: `driver.user_id`, `favoriteDriver.user_id`, `favoriteDriver.driver_id`

#### 남은 한 달 계획

- [ ] 평점 계산 최적화 (컬럼에 저장)
- [ ] 찜한 기사님 목록 조회 페이지 구현

---

### 4.5 리뷰 작성/조회 (원치준) - 2분

#### 기능 설명

- 리뷰 작성: 견적이 수락된 후 리뷰 작성 가능
- 리뷰 조회: 기사님 프로필에서 리뷰 목록 조회
- 리뷰 수정/삭제: 본인이 작성한 리뷰만 수정/삭제 가능

#### 기술적 도전 과제

**1. 리뷰 작성 권한 검증**

- 문제: 견적이 수락된 경우에만 리뷰 작성 가능해야 함
- 해결: Service 레이어에서 비즈니스 로직 검증
- 코드:

```typescript
async function createReview(
  userId: string,
  driverId: number,
  reviewData: CreateReviewDto
) {
  // 1. 해당 사용자가 해당 기사님의 견적을 수락했는지 확인
  const acceptedEstimate = await prisma.estimate.findFirst({
    where: {
      driver_id: driverId,
      request: { user_id: userId },
      status: EstimateStatus.ACCEPTED,
    },
  });

  if (!acceptedEstimate) {
    throw new ApiError(
      403,
      "견적을 수락한 기사님에게만 리뷰를 작성할 수 있습니다",
      "REVIEW_NOT_ALLOWED"
    );
  }

  // 2. 이미 리뷰를 작성했는지 확인
  const existingReview = await prisma.review.findFirst({
    where: {
      user_id: userId,
      driver_id: driverId,
      isDelete: false,
    },
  });

  if (existingReview) {
    throw new ApiError(
      409,
      "이미 리뷰를 작성하셨습니다",
      "REVIEW_ALREADY_EXISTS"
    );
  }

  // 3. 리뷰 생성
  return prisma.review.create({
    data: {
      user_id: userId,
      driver_id: driverId,
      ...reviewData,
    },
  });
}
```

**2. 리뷰 평점 유효성 검증 (구현예정)**

- 문제: 평점은 1~5 사이의 정수여야 함
- 해결: Zod 스키마로 검증
- 코드:

```typescript
export const createReviewSchema = z.object({
  body: z.object({
    review_title: z.string().max(100).optional(),
    review_content: z.string().max(1000).optional(),
    rating: z.number().int().min(1).max(5), // 1~5 사이 정수
  }),
});
```

**3. 리뷰 조회 최적화**

- 문제: 기사님 프로필에서 리뷰 목록 조회 시 성능 이슈
- 해결: 페이지네이션, 필요한 필드만 선택
- 코드:

```typescript
async function getReviewsByDriver(
  driverId: number,
  cursor?: number,
  limit: number = 10
) {
  return prisma.review.findMany({
    where: {
      driver_id: driverId,
      isDelete: false,
    },
    take: limit,
    skip: cursor ? 1 : 0,
    cursor: cursor ? { id: cursor } : undefined,
    orderBy: { createdAt: "desc" },
    select: {
      id: true,
      review_title: true,
      review_content: true,
      rating: true,
      createdAt: true,
      user: {
        select: {
          name: true,
          // 프로필 이미지는 향후 추가
        },
      },
    },
  });
}
```

#### 성능 및 품질 개선

- 리뷰 작성 시 트랜잭션으로 데이터 일관성 보장 - 미구현
- 리뷰 조회 시 `select`로 필요한 필드만 조회 (불필요한 데이터 전송 방지) - 일부 구현
- 리뷰 수정/삭제 시 Soft Delete로 데이터 보존 - 미구현

#### 남은 한 달 계획

- [ ] 리뷰 수정 API 구현
- [ ] 리뷰 이미지 업로드 기능
- [ ] 리뷰 키워드 라이브러리 도입

+) 받은 요청 (기사님) 관리 기능 구현
<img width="733" height="740" alt="image" src="https://github.com/user-attachments/assets/bf38879b-16e2-4785-903b-bd6e1dd82e18" />


---

## 5. 전체적인 기술적 도전 과제

### 5.1 코드 공통화

**asyncWrapper를 통한 에러 처리 일원화**

```jsx
const getMovers = asyncWrapper(
async (req: Request, res: Response) => {
// try-catch 없이 깔끔한 코드
const movers = await moverService.getMovers(...);
return ApiResponse.success(res, movers, "기사님 목록 조회 성공");
}
);
```

- 모든 컨트롤러에서 반복되는 try-catch 제거
- 에러 미들웨어로 일관된 에러 응답

**응답 형식 통일 (ApiResponse)**

```jsx
// 성공 응답
return ApiResponse.success(res, movers, "기사님 목록 조회 성공");
{
  "success": true,
  "message": "기사님 목록 조회 성공",
  "data": [...]
}

// 에러 응답
throw new ApiError(404, "기사님을 찾을 수 없습니다", "MOVER_NOT_FOUND");
{
  "success": false,
  "message": "기사님을 찾을 수 없습니다",
  "code": "MOVER_NOT_FOUND"
}
```

모든 API가 동일한 응답 구조를 반환하여 프론트엔드 개발 편의성 향상

### 5.2 테스트 코드 (Jest)

**현재 상태**: 테스트 코드 미구현  
**계획**:

- 단위 테스트: Service 레이어 비즈니스 로직 테스트
- 통합 테스트: API 엔드포인트 테스트
- Mock을 활용한 Repository 테스트

```typescript
// 예시: 인증 서비스 테스트
describe("AuthService", () => {
  it("should login user with valid credentials", async () => {
    const mockUser = { id: "1", email: "test@test.com", password: "hashed" };
    authRepository.findUserByEmailAndRole = jest
      .fn()
      .mockResolvedValue(mockUser);
    verifyPassword = jest.fn().mockResolvedValue(true);

    const result = await authService.login(
      "test@test.com",
      "password",
      res,
      req,
      "USER"
    );
    expect(result).toHaveProperty("accessToken");
  });
});
```

### 5.3 로깅 시스템 (Winston)

**현재 상태**: 기본 로깅 구현됨  
**개선 계획**:

- 로그 레벨별 파일 분리 (error.log, combined.log)
- 로그 포맷 표준화 (JSON 형식)
- 프로덕션 환경에서 외부 로그 서비스 연동 (CloudWatch, Datadog 등)

```typescript
// Winston 설정 예시
const logger = winston.createLogger({
  level: "info",
  format: winston.format.json(),
  transports: [
    new winston.transports.File({ filename: "error.log", level: "error" }),
    new winston.transports.File({ filename: "combined.log" }),
  ],
});

if (process.env.NODE_ENV !== "production") {
  logger.add(
    new winston.transports.Console({
      format: winston.format.simple(),
    })
  );
}
```

### 5.4 CI/CD 파이프라인

**현재 상태**: 수동 배포  
**계획**:

- GitHub Actions로 자동 배포 파이프라인 구축
- PR 머지 시 자동 빌드 및 테스트 실행
- 메인 브랜치 머지 시 자동 배포

```yaml
# .github/workflows/deploy.yml 예시
name: Deploy
on:
  push:
    branches: [main]
jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      - name: Setup Node.js
        uses: actions/setup-node@v2
      - name: Install dependencies
        run: npm ci
      - name: Run tests
        run: npm test
      - name: Build
        run: npm run build
      - name: Deploy to EC2
        run: |
          # 배포 스크립트
```

### 5.5 장애 대응

**현재 상태**: 기본 에러 처리만 구현됨  
**계획**:

- 헬스 체크 엔드포인트 구현 (`GET /health`)
- 에러 모니터링 도구 연동 (Sentry 등)
- 데이터베이스 연결 풀 최적화
- Rate Limiting 구현 (DoS 공격 방지)

```typescript
// 헬스 체크 예시
app.get("/health", async (req, res) => {
  try {
    await prisma.$queryRaw`SELECT 1`;
    res.status(200).json({
      status: "healthy",
      database: "connected",
      timestamp: new Date().toISOString(),
    });
  } catch (error) {
    res.status(503).json({
      status: "unhealthy",
      database: "disconnected",
      timestamp: new Date().toISOString(),
    });
  }
});
```

---

## 6. 결과 및 회고

### 정량적 결과

**구현 완료 기능** (1개월 기준):

- ✅ 인증/유저 시스템 (회원가입, 로그인, 로그아웃)
- ✅ 프로필 등록
- ✅ 견적 요청 생성
- ✅ 기사님 찾기 (목록 조회, 필터링, 정렬)
- ✅ 리뷰 작성/조회
- ✅ 찜하기 기능

**다음 스프린트 예정**:

- 📋 소셜 로그인
- 📋 프로필 조회/수정
- 📋 프로필 이미지 S3 업로드
- 📋 찜한 기사님 목록 조회
---
- 📋 견적 관리 (유저/기사님)
- 📋 리뷰 수정/삭제 기능
- 📋 알림 기능
---
- 📋 Jest 테스트 코드 작성
- 📋 CI/CD 파이프라인 구축
- 📋 에러 모니터링 도구 연동
- 📋 장애 테스트 후 대응 개선

### 정성적 결과

**잘한 점**:

1. **아키텍처 설계**: 계층형 아키텍처로 관심사 분리, 유지보수성 향상
2. **타입 안전성**: TypeScript + Zod로 런타임/컴파일 타임 모두 타입 보장
3. **에러 처리 표준화**: ApiError/ApiResponse로 일관된 에러 처리
4. **코드 재사용성**: 컴포넌트, 훅, 서비스 레이어 재사용 가능하도록 설계

**아쉬운 점**:

1. **테스트 코드 부재**: 테스트 코드를 작성하지 못해 리팩토링 시 불안함
2. **성능 최적화 미흡**: 평점 계산 등 일부 기능이 매번 계산되어 성능 저하 가능
3. **문서화 부족**: API 문서(Swagger)는 있으나 코드 주석이 부족
4. **에러 모니터링 미구현**: 프로덕션 환경에서 에러 추적이 어려움

### 남은 한 달 목표

**우선순위 1 (필수)**:

1. 프로필 조회/수정 API 완성
2. 견적 요청 관리 (기사님용) 완성
3. 견적 결과 관리 (유저용) 완성
4. 찜한 기사님 목록 조회 UI 구현

**우선순위 2 (중요)**:

1. 알림 기능 구현
2. 프로필 이미지 S3 업로드
3. 리뷰 수정/삭제 기능
4. 테스트 코드 작성 (핵심 기능 위주)

**우선순위 3 (선택)**:

1. CI/CD 파이프라인 구축
2. 에러 모니터링 도구 연동 (Sentry)
3. 성능 최적화 (평점 계산 등)
4. Rate Limiting 구현

### 다음 개선 계획

**기술적 개선**:

- 테스트 코드 작성으로 리팩토링 안전성 확보
- 성능 최적화 (DB 인덱스 추가, 쿼리 최적화)
- 로깅 시스템 고도화 (구조화된 로깅, 외부 서비스 연동)

**기능적 개선**:

- 실시간 알림 (WebSocket 또는 Server-Sent Events)
- 채팅 기능 (기사님-유저 간 소통)
- 결제 시스템 연동

**운영적 개선**:

- CI/CD 파이프라인으로 배포 자동화
- 모니터링 대시보드 구축
- 백업 및 복구 전략 수립

---

## 부록: 주요 파일 구조

### 프론트엔드

```
src/
├── app/              # Next.js App Router
├── components/       # 재사용 가능한 컴포넌트
├── hooks/            # Custom Hooks
├── services/         # API 서비스 레이어
├── libs/             # 라이브러리 설정 (apiClient, validation)
└── utils/            # 유틸리티 함수
```

### 백엔드

```
src/
├── modules/          # 기능별 모듈 (auth, user, movers, request, review)
│   ├── auth/
│   │   ├── auth.routes.ts
│   │   ├── auth.controller.ts
│   │   ├── auth.service.ts
│   │   └── auth.repository.ts
├── middlewares/      # 미들웨어 (인증, 검증, 에러 처리)
├── core/             # 핵심 유틸리티 (ApiError, ApiResponse, security)
├── validators/       # Zod 검증 스키마
└── utils/            # 유틸리티 함수
```

---

**감사합니다**
