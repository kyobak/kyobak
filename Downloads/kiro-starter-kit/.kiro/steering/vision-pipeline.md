---
inclusion: fileMatch
fileMatchPattern: "vision/**"
---
# 비전 파이프라인 구현 지침

## 처리 흐름
1. 2~5초 간격으로 프레임 한 장을 메모리로 읽는다 (간격은 설정값).
2. YOLO nano급 모델로 사람(class 0)을 검출한다. 모델 경로와 신뢰도 임계값은 설정값.
3. `vision/config/<resource_id>.yaml`의 대기 구역 다각형 안에 발 위치(박스 하단 중앙)가 있는 사람만 센다.
4. 10초 이동 중앙값으로 인원 수를 평활화한다.
5. ByteTrack 추적 결과로 통과선(배식구·탑승구)을 넘은 인원을 세고, 최근 5분 기준 분당 처리 인원을 계산한다.
6. `est_wait_min = people_count / throughput_per_min` (처리 인원이 0이면 null).
7. 결과를 HTTPS로 서버에 전송하고 프레임 참조를 즉시 해제한다.

## 설정 파일 예시
```yaml
resource_id: cafeteria-student-hall-a
interval_sec: 3
model: yolo11n.pt
conf_threshold: 0.35
queue_zone: [[120, 400], [620, 400], [640, 700], [100, 700]]
service_line: [[300, 380], [460, 380]]
```

## 모듈 구성
- `capture.py`: 카메라 입력 (파일 저장 금지)
- `detect.py`, `track.py`: 검출과 추적
- `zones.py`: 구역 판정, 통과선 계수
- `metrics.py`: 평활화, 처리율, 대기시간
- `publisher.py`: 서버 전송, 재시도, 오프라인 시 최신 값만 유지
- `eval/`: 공개 데이터셋에서 평균 절대 오차(MAE) 산출

## 품질
- 목표: 평가 세트에서 줄 인원 MAE 2명 이하.
- 신뢰도가 임계값 미만이면 `confidence`를 낮게 보내고, 서버가 대체 표시 여부를 판단한다.
- 순수 계산 함수(zones, metrics)는 카메라 없이 pytest로 테스트할 수 있게 분리한다.
