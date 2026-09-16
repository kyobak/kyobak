---
inclusion: always
---
# 저장소 구조와 명명 규칙

```
docs/            # 주차별 활동지, ADR, 회의록, 정확도 평가 결과, 계획서
  plan/          # 학기 준비계획서 (참고용)
  briefs/        # 기능별 스펙 브리프 (Kiro 스펙 생성 입력)
specs/           # (선택) 과목 제출용 EARS 요구사항 사본
apps/web/        # Next.js PWA
supabase/        # migrations/, seed.sql, RLS 정책
vision/          # 엣지 파이프라인
  config/        # 자원별 대기 구역 다각형·통과선 YAML
  eval/          # 공개 데이터셋 평가 스크립트 (영상 파일 커밋 금지)
jobs/            # 크롤러, 예측 모델
tests/           # 요구사항 인수 테스트
.kiro/           # steering, specs, hooks
README.md  PROMPTS.md  ETHICS.md
```

## 명명
- 요구사항 ID: `REQ-<영역>-<번호>`. 영역은 CORE, VIS, LAU, SHT, CAF, SPC, PRK, RPT, SYS.
- Kiro 스펙의 각 요구사항 제목에 REQ ID를 붙인다. 예: `Requirement 1: REQ-VIS-02 예상 대기시간 반영`
- 인수 테스트 이름에 REQ ID를 포함한다. 예: `test_REQ_VIS_02_wait_time_updates_within_10s`
- 브랜치: `feat/REQ-VIS-02-wait-time`, `fix/REQ-LAU-05-expire-ticket`
- 코드 식별자·파일명은 영어, 문서와 주석은 한국어.

## 핵심 테이블
`resources`, `vision_metrics`, `status_events`, `queue_tickets`, `reports`, `predictions`, `edge_devices`, `push_subs`
