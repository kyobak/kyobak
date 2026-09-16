# Kiro 시작 가이드 (팀 굳건)

## 1. 파일 배치
이 폴더의 내용을 팀 저장소 루트에 그대로 복사하고 커밋한다.
- `.kiro/steering/` : Kiro가 모든 대화에 자동으로 읽는 프로젝트 규칙
- `docs/plan/project-plan.md` : 학기 준비계획서 전문 (참고용, 필요할 때만 #로 첨부)
- `docs/briefs/` : 기능별 스펙 브리프 5개
- `gitignore-additions.txt` : `.gitignore`에 추가할 영상 파일 차단 규칙

steering 파일이 이미 있으므로 Kiro 패널의 "Generate Steering Docs"는 누르지 않는다.
코드가 생긴 뒤 구조가 달라지면 "steering 파일을 현재 코드베이스에 맞게 갱신해줘"라고 요청한다.

## 2. 스펙 생성 순서
브리프 하나당 스펙 하나. 앞 스펙의 요구사항을 팀이 승인한 뒤 다음으로 넘어간다.

| 순서 | 스펙 이름 | 브리프 | 목표 주차 |
|---|---|---|---|
| 1 | core-platform | 01-core-platform.md | 4주차 요구사항, 7주차 설계 |
| 2 | vision-counting | 02-vision-counting.md | 4주차 요구사항, 7주차 설계 |
| 3 | laundry-queue | 03-laundry-queue.md | 4주차 요구사항, 7주차 설계 |
| 4 | shuttle-cafeteria | 04-shuttle-cafeteria.md | 4주차 요구사항, 7주차 설계 |
| 5 | extras | 05-extras.md | 11주차 이후 여유 있을 때 |

## 3. 붙여넣을 프롬프트
Kiro 채팅에서 Spec 모드로 새 스펙을 시작하고 아래를 붙여넣는다. 브리프 파일명만 바꾼다.

```
#01-core-platform.md 이 브리프로 core-platform 스펙을 만들어줘.
- 요구사항은 EARS 형식으로 쓰고, 각 요구사항 제목에 브리프의 REQ ID를 그대로 붙여줘.
- 브리프의 "범위 밖" 항목은 요구사항에 넣지 마.
- 브리프에 없는 요구사항이 필요해 보이면 추가하지 말고 마지막에 질문 목록으로 따로 정리해줘.
- 문서는 한국어로 작성해줘.
```

## 4. 승인 게이트 (사람이 반드시 검토)
1. requirements.md: 팀 회의에서 읽고 수정 → PR로 올려 1명 이상 승인
2. design.md: 아키텍처 ADR과 대조, 개인정보 규칙 위반 여부 확인
3. tasks.md: 태스크마다 담당자를 정하고 GitHub Issue로 옮김
4. 태스크 실행은 9주차부터(6주차 뼈대 작업 제외). Autopilot보다 변경마다 확인하는 방식을 권장

## 5. 과목 규칙과 연결
- 스펙 생성, 설계 변경 등 주요 대화는 `PROMPTS.md`에 날짜, 작성자, 목적, 채택 여부를 기록한다. 채팅 내보내기 기능을 활용해도 된다.
- 4주차 EARS 활동지에는 Kiro가 만든 requirements.md를 팀이 검토·수정한 버전을 사용하고, 어디를 고쳤는지 기록한다.
- 현장 영상, 설문 원본 등 실제 개인정보는 Kiro 채팅에 넣지 않는다.
- 설명하지 못하는 코드는 머지하지 않는다.
