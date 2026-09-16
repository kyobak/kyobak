---
inclusion: always
---
# 기술 스택과 규칙

## 스택
| 영역 | 선택 |
|---|---|
| 웹 클라이언트 | Next.js (App Router), TypeScript strict, Tailwind CSS, PWA + Web Push |
| 백엔드·DB | Supabase (Postgres, Realtime, Edge Functions, Row Level Security) |
| 비전(엣지) | Python 3.11+, OpenCV, Ultralytics YOLO nano급 모델, ByteTrack, Roboflow `supervision` |
| 엣지 기기 | 노트북 웹캠(기본), Raspberry Pi 5 + 카메라 모듈(파일럿) |
| 예측·크롤링 | Python, pandas, scikit-learn, GitHub Actions 스케줄 실행 |
| 배포 | Vercel(웹), Supabase(백엔드) |
| 테스트 | 웹: Vitest, Playwright / Python: pytest |

## 규칙
- 새 라이브러리를 추가하기 전에 이유를 설명하고 확인을 받는다. 위 스택으로 해결되면 추가하지 않는다.
- 모든 Supabase 테이블에 RLS를 켠다. 스키마 변경은 `supabase/migrations/`의 마이그레이션 파일로만 한다.
- 비밀값은 `.env.local`에만 두고, 필요한 키 이름은 `.env.example`에 기록한다. 코드에 키를 하드코딩하지 않는다.
- 엣지 기기는 기기별 API 키로 인증하고, 서버에는 키의 해시만 저장한다.
- 클라이언트는 Supabase Realtime 구독으로 상태를 갱신한다. 폴링은 Realtime이 불가능할 때만 쓴다.
- 시간은 DB에 UTC로 저장하고 화면에서 Asia/Seoul로 표시한다.
- Ultralytics YOLO는 AGPL-3.0이다. 의존성 라이선스를 README의 라이선스 표에 기록한다.
