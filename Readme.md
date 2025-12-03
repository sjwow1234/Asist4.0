# Asist4.0 - AI-Powered Chatbot

Asist4.0은 생성형 AI 기반의 고급 채팅 애플리케이션입니다. 사용자 인증, 채팅 기록 관리, 다양한 AI 모델 선택, 이미지 생성 등의 기능을 제공합니다.

## 주요 기능

- **7가지 AI 모델**: Asist4.0 Fast/Pro/SuperI, Asist3.5 Fast/Pro/SuperI, Asist Art (이미지 생성)
- **사용자 인증**: 회원가입/로그인 (로컬 인증)
- **채팅 기록 관리**: 대화 저장, 조회, 삭제, 이름 변경
- **이미지 생성**: Asist Art 모델로 텍스트 프롬프트에서 이미지 생성
- **파일 다운로드**: 생성된 이미지를 직접 다운로드
- **다크 테마 UI**: 현대적이고 사용하기 편한 인터페이스
- **모바일 반응형**: 모든 기기에서 최적화된 경험
- **독립적 스크롤**: 사이드바와 채팅창이 독립적으로 스크롤
- **실시간 스트리밍**: AI 응답이 타이핑 애니메이션으로 표시
- **코드 블록**: 코드 복사 기능 포함
- **마크다운 렌더링**: 풍부한 텍스트 포맷 지원

## 기술 스택

- **프론트엔드**: React 19, Tailwind CSS 4, TypeScript
- **백엔드**: Express 4, tRPC 11, Node.js
- **데이터베이스**: MySQL/TiDB
- **AI 통합**: Manus LLM API, Image Generation API
- **인증**: 로컬 인증 (bcrypt 기반 비밀번호 해싱)

## 설치 및 실행

### 사전 요구사항

- Node.js 22.13.0 이상
- pnpm 10.4.1 이상
- MySQL 데이터베이스

### 로컬 개발 환경 설정

```bash
# 1. 저장소 클론
git clone <repository-url>
cd asist4_0_chatbot

# 2. 의존성 설치
pnpm install

# 3. 환경 변수 설정
cp .env.example .env.local

# 4. 데이터베이스 마이그레이션
pnpm db:push

# 5. 개발 서버 실행
pnpm dev
```

## 환경 변수 설정

프로젝트 루트에 `.env.local` 파일을 생성하고 다음 변수들을 설정하세요:

```env
# 데이터베이스
DATABASE_URL=mysql://username:password@localhost:3306/asist4_0_chatbot

# JWT 및 세션
JWT_SECRET=your-secret-key-here

# AI API (Manus 플랫폼)
BUILT_IN_FORGE_API_URL=https://api.manus.im
BUILT_IN_FORGE_API_KEY=your-api-key

# 프론트엔드 설정
VITE_APP_TITLE=Asist4.0
VITE_APP_LOGO=/logo.png
```

## 🚀 무료 배포 가이드 (한 번에 배포하기)

### 추천: Railway 또는 Render

프론트엔드, 백엔드, 데이터베이스를 한 번에 배포할 수 있습니다.

#### Railway 배포 (가장 간단)

1. [railway.app](https://railway.app) 접속
2. GitHub 계정으로 로그인
3. "New Project" → "Deploy from GitHub repo" 선택
4. 이 저장소 선택
5. 환경 변수 설정:
   - `DATABASE_URL`: MySQL 연결 문자열 (PlanetScale에서 획득)
   - `JWT_SECRET`: 임의의 긴 문자열
   - `BUILT_IN_FORGE_API_KEY`: Manus API 키
   - `BUILT_IN_FORGE_API_URL`: https://api.manus.im
6. Deploy 버튼 클릭

#### Render 배포

1. [render.com](https://render.com) 접속
2. GitHub 저장소 연결
3. "New Web Service" 생성
4. 환경 변수 설정 (위와 동일)
5. Deploy 버튼 클릭

### 📊 데이터베이스 무료 호스팅

#### PlanetScale (MySQL) - 추천

- 무료 플랜: 월 10GB 스토리지
- [planetscale.com](https://planetscale.com) 가입
- 데이터베이스 생성 후 CONNECTION_STRING 복사
- `DATABASE_URL`로 사용

#### Supabase (PostgreSQL)

- 무료 플랜: 월 500MB 스토리지
- [supabase.com](https://supabase.com) 가입
- 프로젝트 생성 후 연결 문자열 복사
- `DATABASE_URL`로 사용

### 🔑 API 키 획득

#### Manus API

1. [Manus 대시보드](https://manus.im) 접속
2. API 키 생성
3. `BUILT_IN_FORGE_API_KEY`로 설정

### 📋 배포 체크리스트

```
☐ GitHub 저장소 생성 및 코드 푸시
☐ Railway 또는 Render 계정 생성
☐ PlanetScale 또는 Supabase에서 데이터베이스 생성
☐ Manus API 키 획득
☐ 배포 플랫폼에 환경 변수 설정
☐ 배포 실행
☐ 배포된 URL에서 앱 테스트
```

### 🔗 배포 후 테스트

배포 완료 후 다음을 확인하세요:

```bash
# 1. 배포된 URL 접속
# https://your-app.railway.app (또는 render.app)

# 2. 회원가입 테스트
# 3. 채팅 기능 테스트
# 4. 이미지 생성 테스트 (Asist Art 모델)
# 5. 파일 다운로드 테스트
```

### 💡 비용 절감 팁

- **Railway**: 월 $5 크레딧 제공 (대부분의 소규모 앱은 무료)
- **Render**: 무료 플랜 사용 (성능 제한 있음)
- **PlanetScale**: 무료 플랜으로 충분 (월 10GB)
- **Manus API**: 무료 크레딧 제공 (문의 필요)

## 데이터베이스 스키마

### Users 테이블
- `id`: 사용자 ID (자동 증가)
- `username`: 사용자명 (로컬 인증용)
- `passwordHash`: 비밀번호 해시
- `name`: 사용자 이름
- `email`: 이메일
- `role`: 사용자 역할 (user/admin)
- `createdAt`: 생성 날짜
- `updatedAt`: 수정 날짜
- `lastSignedIn`: 마지막 로그인 날짜

### Conversations 테이블
- `id`: 대화 ID (자동 증가)
- `userId`: 사용자 ID (외래키)
- `title`: 대화 제목
- `createdAt`: 생성 날짜
- `updatedAt`: 수정 날짜

### Messages 테이블
- `id`: 메시지 ID (자동 증가)
- `conversationId`: 대화 ID (외래키)
- `role`: 메시지 역할 (user/assistant)
- `content`: 메시지 내용
- `model`: 사용된 AI 모델
- `createdAt`: 생성 날짜

## 프로젝트 구조

```
asist4_0_chatbot/
├── client/                 # 프론트엔드 (React)
│   ├── src/
│   │   ├── components/    # React 컴포넌트
│   │   ├── pages/         # 페이지 컴포넌트
│   │   ├── lib/           # 유틸리티 함수
│   │   ├── App.tsx        # 메인 앱
│   │   └── index.css      # 글로벌 스타일
│   └── public/            # 정적 자산 (logo.png 포함)
├── server/                 # 백엔드 (Express + tRPC)
│   ├── routers.ts         # tRPC 라우터
│   ├── db.ts              # 데이터베이스 쿼리
│   ├── auth.ts            # 인증 로직
│   └── _core/             # 핵심 설정
├── drizzle/               # 데이터베이스 스키마
│   └── schema.ts          # 테이블 정의
└── package.json           # 프로젝트 설정
```

## 개발 명령어

```bash
# 개발 서버 실행
pnpm dev

# 프로덕션 빌드
pnpm build

# 프로덕션 서버 실행
pnpm start

# TypeScript 타입 확인
pnpm check

# 테스트 실행
pnpm test

# 코드 포맷팅
pnpm format

# 데이터베이스 마이그레이션
pnpm db:push
```

## 사용자 인증 흐름

1. **회원가입**: 사용자가 username/password로 계정 생성
2. **비밀번호 해싱**: bcrypt를 사용하여 안전하게 저장
3. **로그인**: 입력된 비밀번호와 저장된 해시 비교
4. **세션 쿠키**: 로그인 성공 시 JWT 기반 세션 쿠키 발급
5. **인증 유지**: 모든 요청에서 쿠키를 통해 사용자 인증 유지

## AI 모델 설명

### Asist4.0 시리즈
- **Fast**: 가볍고 빠른 응답, 일상적인 대화에 최적
- **Pro**: 전문적인 지식 제공, 복잡한 질문 처리
- **SuperI**: 고성능 추론, 논문 작성 수준의 심층 분석

### Asist3.5 시리즈
- Asist4.0보다 한 단계 낮은 성능
- 비용 효율적인 선택

### Asist Art
- 이미지 생성 전용 모델
- 텍스트 프롬프트로 이미지 생성

## 문제 해결

### 데이터베이스 연결 오류
```bash
# 데이터베이스 URL 확인
echo $DATABASE_URL

# 마이그레이션 재실행
pnpm db:push
```

### 인증 오류
- 환경 변수 `JWT_SECRET` 설정 확인
- 쿠키 설정 확인 (HTTPS 환경에서는 `Secure` 플래그 필요)

### AI API 오류
- `BUILT_IN_FORGE_API_KEY` 유효성 확인
- API 할당량 확인

## 기여 방법

1. Fork 저장소
2. 기능 브랜치 생성 (`git checkout -b feature/amazing-feature`)
3. 변경사항 커밋 (`git commit -m 'Add amazing feature'`)
4. 브랜치 푸시 (`git push origin feature/amazing-feature`)
5. Pull Request 생성

## 라이선스

MIT License - 자유롭게 사용, 수정, 배포 가능

## 지원

문제가 발생하면 GitHub Issues에 보고해주세요.

---

**Asist4.0** - 차세대 AI 채팅 경험을 시작하세요! 🚀
