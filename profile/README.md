# Mov2ng

## 팀원 구성

- **김성준**  
  - https://github.com/FLClover-git

- **김연만**  
  - https://github.com/Kimyeonman

- **원치준**  
  - https://github.com/CHIJUNEE

- **조원정**  
  - https://github.com/jwj2087

- **홍명주**  
  - https://github.com/MyeongjuHong

---

## 프로젝트 소개

- **프로젝트명**: Mov2ng – 이사 견적/예약 통합 플랫폼  
- **한 줄 소개**: 이사가 필요한 사용자와 이사업체를 연결하여, 쉽고 빠르게 견적을 비교하고 예약까지 할 수 있는 서비스입니다.
- **프로젝트 기간**: 2024.08.13 ~ 2024.09.03

---

## 기술 스택
| Frontend | Backend | Infra & DB |
| --- | --- | --- |
| ![Next.js](https://img.shields.io/badge/Next.js-000000?style=flat&logo=nextdotjs) <br> ![TailwindCSS](https://img.shields.io/badge/TailwindCSS-06B6D4?style=flat&logo=tailwindcss) <br> ![React Query](https://img.shields.io/badge/React%20Query-FF4154?style=flat&logo=reactquery) | ![Express.js](https://img.shields.io/badge/Express.js-000000?style=flat&logo=express) <br> ![Node.js](https://img.shields.io/badge/Node.js-5FA04E?style=flat&logo=nodedotjs) <br> ![Prisma](https://img.shields.io/badge/Prisma-2D3748?style=flat&logo=prisma) <br> ![PostgreSQL](https://img.shields.io/badge/PostgreSQL-336791?style=flat&logo=postgresql) |  ![Render](https://img.shields.io/badge/Render-000000?style=flat&logo=render) <br> ![Vercel](https://img.shields.io/badge/Vercel-000000?style=flat&logo=vercel) <br> ![AWS](https://img.shields.io/badge/aws) |

- **Frontend**
  - ![Next.js](https://img.shields.io/badge/Next.js-000000?style=flat&logo=nextdotjs)
  - ![TypeScript](https://img.shields.io/badge/Typescript-3178C6?style=flat-square&logo=Typescript&logoColor=white)
  - ![TailwindCSS](https://img.shields.io/badge/TailwindCSS-06B6D4?style=flat&logo=tailwindcss&logoColor=white)
  - ![React Query](https://img.shields.io/badge/React%20Query-FF4154?style=flat&logo=reactquery&logoColor=white)
  - ![React Hook Form](https://img.shields.io/badge/React%20Hook%20Form-%23EC5990.svg?logo=reacthookform&logoColor=white)
  - ![Zod](https://img.shields.io/badge/zod-%233068b7.svg?logo=zod&logoColor=white)
  - Kakao 지도 SDK (`react-kakao-maps-sdk`)
  - Date 관련 라이브러리 (`date-fns`, `react-datepicker`, `react-day-picker`)

- **Backend**
  - ![Express.js](https://img.shields.io/badge/Express.js-000000?style=flat&logo=express) 
  - ![Node.js](https://img.shields.io/badge/Node.js-5FA04E?style=flat&logo=nodedotjs) 
  - ![Prisma](https://img.shields.io/badge/Prisma-2D3748?style=flat&logo=prisma) 
  - ![JWT](https://img.shields.io/badge/jwt-gray?logo=jsonwebtokens)
  - 인증/보안: Argon2, JWT, Helmet, Express-Rate-Limit, Express-Session
  - 문서화: ![Swagger](https://img.shields.io/badge/Swagger-green?logo=swagger&logoColor=white)

  - 로깅: Winston
  - Cron 작업: node-cron
  - 오류 모니터링: Sentry

- **Database & Infra**
  - ![PostgreSQL](https://img.shields.io/badge/PostgreSQL-336791?style=flat&logo=postgresql)
  - AWS S3 (파일 업로드/관리)
  - 환경 변수 관리: Dotenv
  - Vercel (FE 배포)
  - Render (BE 개발용 배포)
  - EC2, RDS (BE 운영용 배포)

- **공통 협업 도구**
  - Git & GitHub (Organization: `Mov2ng`)
  - Discord (팀 채팅)
  - Jira (일정 관리)
  - Notion (문서화)

---

## 파일 구조 (상세)

> FE·BE를 함께 사용하는 Organization 기준으로, 주요 디렉터리/파일과 각 노드가 담당하는 역할을 정리했습니다.

### Frontend (`8--Moving-Mov2ng-FE`)

```bash
8--Moving-Mov2ng-FE
├─ app/                         # Next.js App Router 엔트리 및 전역 레이아웃/페이지
│  ├─ layout.tsx                # 전역 레이아웃, 공통 메타/폰트/헤더/푸터 설정
│  ├─ page.tsx                  # 메인 홈 화면
│  ├─ (routes)/...              # 도메인별 페이지 그룹 (예: 견적 요청/조회, 마이페이지 등)
│  └─ api/                      # Next.js API Route (클라이언트-서버 브리지)
│
├─ src/
│  ├─ components/               # 재사용 가능한 Presentational & Layout 컴포넌트
│  │  ├─ layout/                # 헤더/푸터/전체 레이아웃 관련 컴포넌트
│  │  ├─ common/                # 버튼, 인풋, 모달 등 공용 UI
│  │  └─ domain/                # 견적, 기사, 리뷰 등 도메인별 UI 블록
│  │
│  ├─ features/                 # 특정 기능 단위(페이지 로직+UI)를 묶은 모듈
│  │  ├─ auth/                  # 로그인/회원가입/소셜 로그인 관련 로직 및 뷰
│  │  ├─ estimate/              # 이사 견적 요청/조회 기능
│  │  ├─ movers/                # 이사업체/기사 리스트 및 상세 뷰
│  │  └─ review/                # 리뷰 작성/조회 기능
│  │
│  ├─ app-hooks/                # React Query, 전역 상태(Zustand) 등 커스텀 훅
│  │  ├─ useEstimateQuery.ts    # 견적 관련 데이터 패칭 훅
│  │  ├─ useAuth.ts             # 인증/세션 관리 훅
│  │  └─ ...
│  │
│  ├─ lib/                      # 유틸리티, 클라이언트용 헬퍼 함수
│  │  ├─ api-client.ts          # 백엔드와 통신하는 공통 fetch/axios 래퍼
│  │  ├─ formatter.ts           # 가격/날짜/주소 등 포맷터
│  │  └─ validators.ts          # 클라이언트 단 입력 검증 로직 (Zod 등)
│  │
│  ├─ stores/                   # Zustand 전역 상태 관리
│  │  ├─ estimateStore.ts       # 견적 폼/단계 진행 상태
│  │  ├─ userStore.ts           # 로그인 사용자 정보
│  │  └─ uiStore.ts             # 모달, 토스트 등 UI 상태
│  │
│  └─ styles/                   # 전역/모듈 스타일(SCSS, Tailwind 설정 등)
│     ├─ globals.scss           # 전체 글로벌 스타일
│     ├─ variables.scss         # 컬러/타이포/spacing 변수
│     └─ mixins.scss            # 공용 mixin, 유틸 스타일
│
├─ public/                      # 정적 리소스 (이미지, 아이콘, 폰트 등)
│  ├─ images/
│  └─ favicon.ico
│
├─ sentry.client.config.ts      # 클라이언트 Sentry 설정
├─ sentry.server.config.ts      # 서버 Sentry 설정
├─ sentry.edge.config.ts        # Edge 런타임용 Sentry 설정
└─ package.json                 # FE 의존성 및 npm 스크립트 정의
```

### Backend (`8--Moving-Mov2ng-BE`)

```bash
8--Moving-Mov2ng-BE
├─ src/
│  ├─ app.ts                    # Express 애플리케이션 엔트리, 미들웨어/라우터 등록
│  │
│  ├─ config/                   # 환경/DB 설정
│  │  ├─ env.ts                 # 환경 변수 로딩 및 검증
│  │  └─ db.ts                  # Prisma/DB 연결 설정
│  │
│  ├─ constants/                # 공통 상수 정의
│  │  ├─ http.ts                # HTTP 상태 코드/메시지
│  │  ├─ estimate.ts            # 견적 상태, 타입 상수
│  │  ├─ pagenation.ts          # 페이지네이션 관련 기본값
│  │  └─ roles.ts               # 권한/역할(Role) 상수
│  │
│  ├─ core/
│  │  ├─ http/
│  │  │  ├─ ApiError.ts         # 공통 에러 객체 정의
│  │  │  └─ ApiResponse.ts      # 공통 응답 포맷 래퍼
│  │  └─ security/
│  │     └─ password.ts         # 패스워드 해시/검증(Argon2) 유틸
│  │
│  ├─ middlewares/              # Express 미들웨어 모음
│  │  ├─ auth.middleware.ts     # 인증(JWT/세션) 검증
│  │  ├─ role.middleware.ts     # 권한(Role) 체크
│  │  ├─ estimate.middleware.ts # 견적 관련 요청 전처리
│  │  ├─ rateLimit.middleware.ts# 요청 속도 제한
│  │  ├─ validate.middleware.ts # 요청 DTO 검증(Zod 등)
│  │  └─ error.middleware.ts    # 전역 에러 핸들러
│  │
│  ├─ modules/                  # 도메인 별 모듈(Controller/Service/Repository/DTO)
│  │  ├─ auth/                  # 로그인·회원가입·토큰 재발급 등 "로그인/계정" 기능을 제공
│  │  │  ├─ auth.controller.ts  # 인증 관련 HTTP 엔드포인트
│  │  │  ├─ auth.service.ts     # 로그인/회원가입/토큰 발급 비즈니스 로직
│  │  │  ├─ auth.repository.ts  # 유저 정보 조회/저장(DB 접근)
│  │  │  ├─ auth.dto.ts         # 요청/응답 DTO 정의
│  │  │  └─ auth.routes.ts      # /auth 라우트 정의
│  │  ├─ estimate/              # 사용자가 이사 견적을 "요청·수정·조회"하는 기능을 제공
│  │  ├─ history/               # 사용자의 과거 이사 견적/요청 "이력 조회" 기능을 제공
│  │  ├─ movers/                # 이사업체·기사 "프로필 및 정보"를 관리하고 노출하는 기능을 제공
│  │  ├─ notice/                # 서비스 내 "공지사항 목록/상세"를 조회하는 기능을 제공
│  │  ├─ profile/               # 회원 "기본 정보·연락처·주소" 등의 프로필 관리 기능을 제공
│  │  ├─ request/               # 견적 이후 실제 "이사 요청·예약 흐름"을 관리하는 기능을 제공
│  │  ├─ review/                # 사용자가 남기는 "이사 후기 작성·수정·조회" 기능을 제공
│  │  ├─ sample/                # 샘플·테스트용 API (개발자용 예제, 실사용 기능 아님)
│  │  └─ upload/                # 사진·문서 등 "파일 업로드"를 처리(S3 업로드/URL 발급 등)
│  │
│  ├─ services/
│  │  ├─ discordBot.ts          # 서버 상태/알림을 Discord로 보내는 Bot 서비스
│  │  └─ s3/
│  │     ├─ s3Client.ts         # AWS S3 클라이언트 설정
│  │     ├─ s3FileKey.ts        # 파일 키/폴더 규칙 관리
│  │     └─ presignedUrl.ts     # 업로드용 Presigned URL 생성 로직
│  │
│  ├─ utils/                    # 공용 유틸 함수
│  │  ├─ asyncWrapper.ts        # 비동기 컨트롤러 에러 랩핑 헬퍼
│  │  ├─ jwt.ts                 # JWT 토큰 생성/검증 유틸
│  │  ├─ logger.ts              # Winston 기반 로거
│  │  ├─ origin.utils.ts        # CORS Origin 관련 유틸
│  │  └─ region.utils.ts        # 지역/구/동 매핑 유틸
│  │
│  ├─ validators/               # 요청 검증 스키마
│  │  ├─ auth.validator.ts
│  │  ├─ profile.validator.ts
│  │  ├─ review.validator.ts
│  │  └─ ...
│  │
│  └─ types/
│     └─ express.d.ts           # Express Request/Response 커스텀 타입 확장
│
├─ prisma/
│  ├─ schema.prisma             # DB 스키마 정의
│  ├─ migrations/               # Prisma 마이그레이션 기록
│  ├─ seed.ts                   # 초기 데이터 시드 스크립트
│  └─ reset.ts                  # 개발용 DB 초기화 스크립트
│
├─ jest.config.ts               # Jest 테스트 설정
├─ jest.setup.ts                # 테스트 공통 설정
├─ prisma.config.ts             # Prisma CLI 설정
└─ package.json                 # BE 의존성, 빌드/테스트/마이그레이션 스크립트 정의
```

---

## 프로젝트 회고록

### 김연만 – 백엔드 리더 / ERD 설계

#### 2. 👤 담당한 작업

- **담당 Role**: 백엔드 리더, ERD 설계 등
- **주요 기여**
  - history 테이블(트리거 구현)
  - 알림 API 제작
  - 견적 요청(기사님) API 제작
  - ERD 제작 및 Prisma 설계

#### 3. 🧰 기술적 성과

- **사용한 기술 스택**
  - **FE**: 담당 X
  - **BE**: 트리거를 통한 history 테이블 자동 생성(백엔드 유지관리), 여러 API 설계 및 구현
  - **Infra/DevOps**: 담당 X
  - **기타**: ERD 설계
- **구현한 주요 기능**
  - history 테이블(트리거 구현)  
    - 데이터 확인과 백엔드에 빈 값이 들어가는지 등을 추적하기 위해 history 테이블과 DB 트리거를 설계·구현하여 코드 보완성과 유지보수성을 높임
  - 알림·견적 요청(기사님) API 설계 및 구현  
    - 기사님 대상 알림 API, 견적 요청 API를 백엔드에서 설계 및 구현

#### 4. 🛠️ 문제점 및 해결 과정

- **문제 1 – 마이그레이션 오류**
  - **S**: 마이그레이션 과정에서 오류 발생
  - **T**: 트리거 설정 및 스키마 설정을 올바르게 구성해야 함
  - **A**: 다른 폴더에 git clone 후 초기화된 상태에서 마이그레이션 테스트를 반복 수행
  - **R**: 오류 동작을 재현·해결하며 마이그레이션이 안정적으로 동작하도록 수정

#### 5. 🤝 협업 및 피드백

- **협업 방식**: 오류나 회의가 있을 때 Discord나 ZEP에서 실시간 회의 진행
- **커뮤니케이션에서 배운 점**: 대화를 자주 나누는 것이 프로젝트 방향 정리와 문제 해결에 큰 도움이 됨을 체감
- **피드백 & 반영**
  - API 데이터 형태 누락 → 즉시 필드 추가 및 응답 스키마 보완
  - 마이그레이션 충돌 → 원격 저장소를 새로 clone 후 마이그레이션 순서를 재정리하여 충돌 해결

#### 6. 🧹 코드 품질 및 최적화

- **디자인 원칙 / 패턴**
  - 트리거를 통한 history 테이블 도입으로 코드 수정 없이도 변경 이력을 추적할 수 있게 하여 유지보수성을 높임
- **향후 보완 아이디어**
  - history 데이터에 인덱스를 추가하여 조회 성능 최적화
  - 운영 환경에서 history 용량 관리(보관 주기, 아카이빙 정책 등) 도입

#### 7. 🔮 향후 개선 사항 및 제안

- **개선 가능 항목**
  - 수정·삭제 파이프라인 구축(동시 수정 시 데드락/경합 상황을 제어하는 트랜잭션/락 전략)
- **차기 프로젝트 아이디어**
  - 검색 인덱스 및 전문 검색(예: Full Text Search) 기능을 도입해 데이터 검색 속도 개선

#### 8. 🌟 프로젝트 총평

- **가장 성장한 부분**
  - Express 기반 마이그레이션 및 Prisma 마이그레이션을 직접 경험하면서, 기존에 GUI SQL 툴 중심으로 작업할 때는 느끼기 어려웠던 스키마/마이그레이션 설계 관점을 체득
- **아쉬운 점 / 강화하고 싶은 역량**
  - 프론트엔드 개발 비중이 낮았던 점
  - 다양한 라이브러리와 스택을 더 사용해보며 프론트엔드 역량을 강화하고자 함

---

### 원치준 – 프론트엔드 리더 & 풀스택

#### 2. 👤 담당한 작업

- **담당 Role**: 프론트엔드 리더 & 풀스택
- **주요 기여**
  - 프론트엔드 PR 승인 및 브랜치 관리
  - 일반 유저 – 견적 관리 페이지 풀스택 구현
  - 일반 유저 – 리뷰 페이지 풀스택 구현

#### 3. 🧰 기술적 성과

- **사용한 기술 스택**
  - **FE**: Node.js, TypeScript, TanStack Query, Next.js, React, Tailwind CSS
  - **BE**: PostgreSQL, Jest, Swagger, Express.js, Node.js, TypeScript
- **구현한 주요 기능**
  - 리뷰 작성 기능  
    - 리뷰 작성 시 백엔드에서 Zod 검증을 통해 유효성 검사 수행  
    - 사용자가 의도한 값만 저장되도록 폼·백엔드 검증을 설계
  - 견적 확정 UX 개선  
    - 견적 확정 시 `invalidateQueries`를 이용해 대기 중인 견적 및 기존 견적 데이터를 즉시 최신화하여 UX 개선

#### 4. 🛠️ 문제점 및 해결 과정

- **문제 1 – DB에는 데이터가 있는데 빈 배열로 조회되는 오류**
  - **S**: 기사님이 견적을 보냈을 때 DB에는 데이터가 잘 저장되지만, 조회 API에서는 빈 배열로 내려오는 문제 발생
  - **T**: DB는 정상인데 응답이 빈 배열인 이유를 찾는 것
  - **A**: 엔드포인트와 GET 요청 메서드 조건을 재검토하여 status 조건이 기획과 다르게 설정되어 있음을 발견  
    (대기중 견적 status가 `accepted`가 아닌데도 `pending`으로 조회하도록 구현되어 있었음)
  - **R**: 올바른 status 조건으로 수정하여 대기중 견적 조회가 정상 동작하도록 해결

#### 5. 🤝 협업 및 피드백

- **협업 방식**
  - 간단한 오류 및 PR 충돌 시 Discord 채팅 우선, 필요 시 ZEP에서 음성 소통
- **커뮤니케이션에서 배운 점**
  - 팀장이 바쁜 상황에서도 팀원의 에러를 우선순위에 따라 빠르게 해결하는 모습에서, 작업 우선순위 정리와 팀 내 서포트의 중요성을 배움
- **피드백 & 반영**
  - E2E 테스트 과정에서 크리티컬 이슈를 먼저 짚어주어, 우선순위를 재조정하고 빠르게 버그 수정 완료

#### 6. 🧹 코드 품질 및 최적화

- **디자인 원칙 / 패턴**
  - 컴포넌트 관심사 분리, 커스텀 훅 분리, HYBRID ARCHITECTURE 적용으로 도메인별 기능 유지보수성 향상
- **관련 PR 링크**
  - https://github.com/Mov2ng/8--Moving-Mov2ng-FE/pull/13

#### 7. 🔮 향후 개선 사항 및 제안

- **개선 가능 항목**
  - TanStack Query key의 상수화가 부족해 유지보수 난이도가 높아질 수 있음 → 키 상수화를 통해 쿼리 구조를 정리할 예정
- **차기 프로젝트 아이디어**
  - 리뷰 키워드 라이브러리를 도입하여, 리뷰 조회 시 핵심 단어를 노출해 빠른 정보 전달과 서비스 품질 향상을 목표

#### 8. 🌟 프로젝트 총평

- **가장 성장한 부분**
  - 컴포넌트 재사용과 UX 개선을 염두에 둔 개발 사고 정착
  - Zod 기반 유효성 검증을 통해 프로젝트 전반의 품질을 끌어올린 경험
- **아쉬운 점 / 강화하고 싶은 역량**
  - 상수화 및 성능 개선을 고려한 클린 코드 작성 역량
  - Zustand 등 전역 상태 관리를 적극 활용해 프로젝트 품질을 한 단계 더 끌어올리고자 함

---

### 조원정 – 기사님 찾기 & 배포/운영

#### 2. 👤 담당한 작업

- **담당 Role**: 기사님 찾기 API 구현, 기사님 찾기 페이지 구현, 배포 및 자동화 운영
- **주요 기여**
  - BE: 기사님 찾기 API 구현, 찜하기 기능(POST/DELETE), 조건부 로그인 인증 미들웨어
  - FE: 기사님 찾기 페이지, 기사님 상세 페이지 구현, TanStack Query를 이용한 API 호출
  - Infra: AWS EC2 + RDS 배포, GitHub Actions 기반 CI/CD 구축

#### 3. 🧰 기술적 성과

- **사용한 기술 스택**
  - **FE**
    - Next.js(App Router 기반), TanStack Query, TypeScript
  - **BE**
    - Node.js + Express, TypeScript
  - **Infra/DevOps**
    - AWS EC2, AWS RDS, GitHub Actions
- **주요 기술 성과**
  - 기사님 찾기 API 및 무한 스크롤 대응 응답 구조 정제
  - Render/EC2/RDS 환경에서의 성능 이슈 분석 및 네트워크/리소스 문제 해결
  - GitHub Actions + EC2 조합으로 CI(빌드)와 런타임 서버 역할 분리 및 릴리스 구조 개선

#### 4. 🛠️ 문제점 및 해결 과정

- **문제 1 – 무한 스크롤과 응답 구조 불일치**
  - API 응답이 `{ ok, data: { list } }` 형태라 `useInfiniteQuery`에서 필요한 `list` 데이터 구조와 맞지 않는 문제를, `queryFn` 레벨에서 `response.data`만 반환하도록 정제하여 해결
- **문제 2 – Render 배포 환경에서의 API 지연**
  - 타임스탬프 로깅, DBeaver로 쿼리 시간 측정, 환경별 응답 시간 비교를 통해 DB·코드가 아닌 Render 프리티어 리소스 한계가 원인임을 파악
- **문제 3 – EC2 ↔ RDS 네트워크 이슈**
  - EC2/RDS 보안 그룹 인바운드/아웃바운드를 단계적으로 점검하고, RDS 보안 그룹의 소스를 EC2 보안 그룹으로 한정하여 안정적인 통신 구성
- **문제 4 – GitHub Actions 배포 시 EC2 메모리 부족(OOM)**
  - 단기적으로 swap 설정, 근본적으로는 빌드를 GitHub Actions에서 수행하고 EC2는 빌드 결과만 배포·실행하도록 파이프라인 구조를 개편

#### 6–8. 협업, 개선점, 총평

- 협업 과정에서 네트워크/배포 이슈를 팀과 공유하며 문제를 구조적으로 분해하는 연습을 함
- 대용량 데이터와 트래픽 증가를 대비한 인덱스 최적화, 캐싱 계층 도입, Docker 기반 배포 등 확장성 있는 아키텍처에 관심을 확장
- CI/CD와 인프라 운영 전반에 대한 이해도가 크게 향상된 프로젝트로 평가

---

### 홍명주 – 팀 리드 & 풀스택 (아키텍처/인증/프로필)

#### 2. 👤 담당한 작업

- **담당 Role**: 팀 리드, 풀스택 개발자(아키텍처 설계, 인증/인가, 프로필)
- **주요 기여**
  - FE 계층형 아키텍처 설계 및 구현(Hook → Service → API Client)
  - API 클라이언트 래퍼 구현(자동 토큰 갱신, 에러 처리 통일)
  - React Query 커스텀 훅 구현(`useApiQuery`, `useApiMutation`)
  - S3 Presigned URL 기반 파일 업로드 구조 설계 및 구현
  - BE 계층형 아키텍처 설계 및 구현(Routes → Middleware → Controller → Service → Repository)
  - 에러 처리 표준화(`ApiError`, `ApiResponse`)
  - JWT 기반 인증 시스템 구축(Access/Refresh Token, HTTP-only 쿠키)
  - CORS 및 쿠키 설정(로컬/개발/운영 환경별 분기)
  - 프로필 등록/조회/수정 API 구현(역할별 동적 검증)
  - Rate Limiting 적용, Swagger API 문서화

#### 3. 🧰 기술적 성과

- **사용한 기술 스택**
  - FE: Next.js 16(App Router), React 19, TypeScript, TanStack Query, React Hook Form + Zod, Tailwind CSS
  - BE: Express 5, TypeScript, Prisma, PostgreSQL, JWT, Argon2, Zod, Swagger, Express Rate Limit
  - Infra/DevOps: Vercel, Render, AWS EC2/RDS, Sentry, AWS S3
  - 기타: Discord Bot, Winston
- **구현한 주요 기능**
  - 역할 기반 이중 인증 시스템(이메일+역할 복합 유니크, USER/DRIVER 역할 분리 및 전환 지원)
  - 스마트 매칭 시스템(서비스 카테고리+지역 기반 기사님 매칭)
  - 견적 요청–응답 워크플로우 전체 설계
  - 커서 기반 페이지네이션과 Raw Query 정렬 최적화
  - 리뷰/평점 시스템, 역할별 동적 프로필 관리

#### 4. 🛠️ 문제점 및 해결 과정

- **파일명 컨벤션 논의**  
  - `request.user.**.ts`, `request.driver.**.ts`로 통일하여 버그 추적과 유지보수성 향상
- **쿠키 path/SameSite 문제로 인한 인증 이슈**  
  - `path: "/"` 명시 및 환경별 SameSite/secure 옵션 분기(`strict` vs `none`)로 해결
- **토큰 갱신 로직 중복**  
  - `apiClient` 레벨에서 토큰 만료 검사 및 자동 갱신, 401 발생 시 재시도 로직을 중앙화
- **Next.js App Router의 SSR/CSR 혼합으로 인한 hydration mismatch**  
  - `isMounted` 플래그와 `RouteGuard`/`useMe` 구조 개선으로 SSR/CSR 초기 렌더 결과를 일치시킴
- **복잡한 접근 제어 로직(RouteGuard)**  
  - 경로를 상수 그룹으로 분류하고, 인증 → 권한 → 프로필 유무 순서로 분기하는 단일 가드로 정리

#### 5–7. 협업, 코드 품질, 개선점

- Git Flow, PR 리뷰, Discord/Notion/Jira를 활용한 협업 문화 정착
- 계층형 아키텍처, Repository 패턴, 전략 패턴, 커스텀 훅 분리 등으로 가독성과 재사용성 향상
- TanStack Query 캐싱, 토큰 자동 갱신, Rate Limiting, 쿼리 최적화 등을 통해 성능과 보안을 동시에 고려
- 향후 TDD, CI/CD, 모니터링/캐싱/마이크로서비스/실시간 통신/고급 인증 방식 도입을 목표로 설정
- 관련 PR: https://github.com/Mov2ng/8--Moving-Mov2ng-BE/pull/88  
  코드 리뷰: https://www.notion.so/2ed22fc65e1080cd8e16c6f9ba253536?pvs=21

#### 8. 🌟 프로젝트 총평

- 아키텍처 설계부터 테스트, 배포까지 전체 웹 개발 라이프사이클을 경험하며 웹·브라우저 보안 이해도가 크게 향상
- JIRA 스프린트 방식의 장점을 체감하며, 향후 사이드 프로젝트에서도 단위 기간을 명확히 두는 개발 문화를 적용하고자 함
- AWS/CI/CD 영역은 향후 프로젝트에서 더 깊이 경험해보고 싶은 부분으로 남김

---

## 구현 홈페이지

- **서비스 링크**: 
  - https://mov2ng.store 

---

## **발표 자료

<img width="1437" height="807" alt="image" src="https://github.com/user-attachments/assets/a7a3b85b-0221-4705-9537-8d4147dc24dd" />

<img width="1437" height="808" alt="image" src="https://github.com/user-attachments/assets/fdb11f42-2e01-47e9-9633-9f4109c6c248" />

<img width="1436" height="808" alt="image" src="https://github.com/user-attachments/assets/111374ae-f35b-4dc7-a23f-718ed99c44f5" />

<img width="1436" height="807" alt="image" src="https://github.com/user-attachments/assets/afe74500-6a84-4743-905c-9c987956f0ba" />

<img width="1435" height="806" alt="image" src="https://github.com/user-attachments/assets/2cff8db2-9f87-45f2-a697-a32fce2604ed" />

<img width="1436" height="807" alt="image" src="https://github.com/user-attachments/assets/19fd24e8-52cc-431b-8e10-cd532e3979dd" />

<img width="1436" height="807" alt="image" src="https://github.com/user-attachments/assets/cf193ae9-bd47-4073-b668-408511b01022" />

<img width="1435" height="808" alt="image" src="https://github.com/user-attachments/assets/ab231d3d-b2cb-405b-9a92-9b3f8e12e8e1" />

<img width="1435" height="807" alt="image" src="https://github.com/user-attachments/assets/4e0c3e71-34db-4169-a45a-11bc874de7b9" />

<img width="1434" height="805" alt="image" src="https://github.com/user-attachments/assets/31239351-168a-47e2-8646-e409cae4e7a1" />

<img width="1436" height="807" alt="image" src="https://github.com/user-attachments/assets/94e1fdd1-8251-44e8-a33b-f821f9c0f15e" />

<img width="1435" height="808" alt="image" src="https://github.com/user-attachments/assets/5ccd93db-9ba4-431d-925f-88f01f89e832" />

<img width="1436" height="808" alt="image" src="https://github.com/user-attachments/assets/b55662be-5e32-4122-aa35-693bc1cda228" />

<img width="1437" height="808" alt="image" src="https://github.com/user-attachments/assets/f16e0fd2-bf7f-4d26-884e-72c7c245eab2" />

<img width="1435" height="805" alt="image" src="https://github.com/user-attachments/assets/16b8becd-6af3-4c4b-b747-1c32225f128a" />

<img width="1434" height="806" alt="image" src="https://github.com/user-attachments/assets/21e5dd96-6ceb-4d42-ae92-44f6a4151d5d" />

<img width="1436" height="807" alt="image" src="https://github.com/user-attachments/assets/bd95b3ba-db81-4e01-a2a4-ad3549d23f57" />

<img width="1437" height="807" alt="image" src="https://github.com/user-attachments/assets/cffc388c-7d30-4a4b-a61a-5e9dff5c6757" />

<img width="1435" height="806" alt="image" src="https://github.com/user-attachments/assets/4c9b930f-8df1-4766-b14c-4ec3121b8d0c" />

<img width="1435" height="807" alt="image" src="https://github.com/user-attachments/assets/e51469b9-eaf0-4241-a924-73b8f27a569c" />

<img width="1435" height="807" alt="image" src="https://github.com/user-attachments/assets/1979a93d-6739-4434-af39-596f0f53e782" />

<img width="1436" height="807" alt="image" src="https://github.com/user-attachments/assets/32438124-a22e-499c-b1d4-21fc3c7c672e" />

<img width="1434" height="806" alt="image" src="https://github.com/user-attachments/assets/41c17edd-8f8d-475e-b669-0df7c0297907" />

<img width="1438" height="808" alt="image" src="https://github.com/user-attachments/assets/0a910a04-1678-4e2c-90ec-8e7f5d0470bb" />

<img width="1435" height="806" alt="image" src="https://github.com/user-attachments/assets/a86d5736-4d5f-43a2-9963-e65633ecadd2" />

<img width="1436" height="808" alt="image" src="https://github.com/user-attachments/assets/4c54898c-5524-4a11-8879-c1ffc9f12c4b" />

<img width="1435" height="808" alt="image" src="https://github.com/user-attachments/assets/a201bfa8-1bec-4c3e-a30e-4a5d42a04eb3" />

<img width="1436" height="807" alt="image" src="https://github.com/user-attachments/assets/e4f28cad-7d94-4163-8853-2e11d33c25b6" />

<img width="1437" height="807" alt="image" src="https://github.com/user-attachments/assets/47e5ad1b-f999-4f51-b5f0-523a98bd0c49" />

<img width="1436" height="808" alt="image" src="https://github.com/user-attachments/assets/dce1b7fc-e959-4188-b143-46c14b77c1a9" />

<img width="1437" height="808" alt="image" src="https://github.com/user-attachments/assets/0c0f075c-ca2c-45de-abee-0cde7bb53842" />

<img width="1435" height="806" alt="image" src="https://github.com/user-attachments/assets/9f6b7432-c802-42ee-a582-8580cec4ac9b" />

<img width="1436" height="808" alt="image" src="https://github.com/user-attachments/assets/f198a5f4-887c-4433-b495-5398e4babb09" />

<img width="1437" height="808" alt="image" src="https://github.com/user-attachments/assets/408e9490-b1f8-4ff4-8d7a-723ee68ac40e" />


  
