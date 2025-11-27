# Dupilot

## 서비스 목적
- 크래프톤 정글 10기 나만의 무기 1조의 AI 자동 더빙 서비스.
- 한 번의 업로드로 영상 더빙 생성 → 브라우저에서 바로 편집 → 보이스를 사고팔 수 있는 마켓까지 이어지는 워크플로우 제공.

## 팀 멤버
- [진주영](https://github.com/jjy3385)
- [정성원](https://github.com/seongwonjung)
- [안준](https://github.com/anjun206)
- [김현수](https://github.com/kimhyunso)
- [장윤호](https://github.com/yunojang)

## 개발 기간
- 2025.10.24 ~ 2025.11.29

## 기술 스택
- Frontend: React 18, Vite, TypeScript, TailwindCSS, Radix UI, React Query, Zustand, Zod, MSW, Vitest/Playwright.
- Backend: FastAPI, MongoDB, boto3(S3), SQS 기반 비동기 잡 큐, Uvicorn, Docker/Compose.
- STT/TTS Worker: WhisperX STT, CosyVoice TTS, ffmpeg 파이프라인, CUDA 기반 Docker 멀티스테이지 빌드.
- Infra/툴링: Docker Compose(dev/prod), GitHub Actions(CI), Husky + lint-staged, Prettier/ESLint.

## 아키텍처
- Frontend (React/Vite): 프로젝트 생성·목록·편집 UI, 타임라인/파형 기반 더빙 편집, API 연동/캐싱(React Query).
- Backend (FastAPI): 인증/프로젝트/작업 API 게이트웨이, MongoDB 저장소, S3 업로드·결과 관리, SQS로 STT/TTS 파이프라인 트리거.
- STT-TTS-Worker: WhisperX로 음성 인식 → 번역/싱크 → CosyVoice 등 TTS로 합성 → ffmpeg로 mux하여 더빙 영상/오디오 산출.
- 공유 리소스: `data/`와 `models/` 볼륨으로 입력/중간/출력/모델 캐시 관리, S3 업로드 경로는 환경변수로 설정.

## 기능
### 영상 자동 더빙
- 영상/오디오 업로드 후 STT → 번역 → TTS → 오디오/영상 mux까지 자동 처리.
- Job 큐(SQS) 기반 비동기 처리, 결과 메타데이터/파일 경로를 API로 반환.

### 에디터
- 브라우저에서 타임라인·파형을 보며 클립 단위로 편집.
- 프리뷰 재생, 구간 선택/수정, 추후 멀티트랙·다국어 확장 준비.

### 보이스 마켓
- 커스텀 보이스 업로드/적용을 위한 마켓 플레이스 컨셉.
- 향후 거래/적용 플로우 연동 예정(보이스 메타데이터 관리 포함).

## 포스터
![Dupilot 포스터](../resource/Dupilot-poster.jpg)

## 시연 영상
<video src="../resource/Dupilot-Showcase.mp4" controls width="100%">
  Your browser does not support the video tag.
</video>
