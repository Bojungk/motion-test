# scenes — mission-approved (director)

확정: **A안** (2026-11-08 사용자 선택)
600f = 20초 · 30fps · 전환은 모두 컷 (motion.md 5장). 글줄은 화면에 있는 문구만 쓴다.

---

## A안 v3 — 15초 · 장면마다 타이포 짝 (2026-11-08 사용자 요청) → `video-v3/`

v2와 같은 컷 · 길이 · 효과음. 각 장면의 이미지 옆에 그 화면의 문구를 타이포로 놓는다 (문구는 03 · 04 화면 · 부품에 있는 것만).
배치: 제목 안전 영역 80% (x 192–1728). 이미지와 글 사이 · 글줄 사이 간격 = `space-large` 32 × 2.8 = 90 / `space-content` 16 × 2.8 = 45.

| # | 이미지 | 타이포 (토큰) | 효과 |
|---|---|---|---|
| 1 | — | "이번 달 미션" `video-headline` + "반복 업무를 줄이는 AI 자동화" `video-title` | typewriter → 둘째 줄 `motion-appear` |
| 2 | `03-mission` 폰 오른쪽 | 왼쪽: "결과물 제출" `video-eyebrow` · "자동화 파일과 적용 전·후 사례를 제출해주세요." `video-title` | `motion-screen` · 글줄 `motion-list` · push-in 1.3배 |
| 3 | `mission-card` 왼쪽 | 오른쪽: "50%" `video-headline` · "2/4 단계 완료" `video-title` · "9월 30일 마감" `video-label` muted | 카드 `motion-appear` · 숫자 0→50% 진행 바와 같이 (`duration-long`) · 글줄 `motion-list` |
| 4 | `button-submit` 가운데 아래 | 위: "결과물 제출" `video-headline` · 아래: "파일과 적용 사례를 함께 제출해주세요." `video-body` muted | `motion-list` → 버튼 `motion-exit` |
| 5 | `04-approved` 폰 왼쪽 | 오른쪽: "승인 완료" `video-eyebrow` · "결과물이 승인되어 내 자산에 등록됐어요." `video-title` | 컷 → 글줄 `motion-list` · push-in 1.3배 (배지 쪽) |
| 6 | `badge-approved` | "미션을 완성했어요!" `video-headline` | typewriter (v2와 같음) |
| 7 | 로고 | — | v2와 같음 |

## A안 v2 — 15초 (2026-11-08 사용자 요청: 15초 · 효과음 · push-in · typewriter)

450f = 15초. 박자 120BPM = 15f마다 한 박, 컷은 모두 박 위 (60 · 165 · 225 · 270 · 345 · 390f). 음악 없음 (HeyGen CLI가 Windows 미지원) → 효과음이 박을 만든다.

| # | 시작 f | 길이 f | 화면/부품 | 움직임 · 카메라 | 효과음 | 참조 |
|---|---|---|---|---|---|---|
| 1 | 0 | 60 | 글줄 `video-headline` "이번 달 미션" | typewriter `stagger-type` 4f × 7글자 → 머묾 | 타이핑 | R1 00:00 · A 00:05 글자 입력 |
| 2 | 60 | 105 | `03-mission.png` 폰 | `motion-screen` 40f → `hold-beat` → push-in 1.3배 (미션 카드 쪽) 40f | 휙 · 부드러운 휙 | R2 00:03 · R4 00:09 |
| 3 | 165 | 60 | `mission-card.html` ×2.8 | `motion-appear` → 진행 바 24f | 팝 | R3 00:05 |
| 4 | 225 | 45 | `button-submit.html` `submit` | `motion-appear` → `motion-exit` | 팝 · 클릭 | R5 00:13 |
| 5 | 270 | 75 | `04-approved.png` 폰 | 컷 → `hold-beat` → push-in 1.3배 (배지 쪽) 40f | 부드러운 휙 | R4 00:09 |
| 6 | 345 | 45 | `badge-approved.html` ×2.8 + 글줄 "미션을 완성했어요!" | 배지 `motion-appear` · 글줄 typewriter 4f × 10글자 | 차임 · 타이핑 | R6 00:14 |
| 7 | 390 | 60 | 엔드 카드 로고 | `motion-appear` → 머묾 | 임팩트 | R8 00:22 |

---

## A안 — 레퍼런스 뼈대 그대로 (추천, 20초 v1)
글줄 → 폰 → 부품 → 폰 + 카메라 → 완료 → 엔드. A의 R1~R8 순서를 따른다.

| # | 시작 f | 길이 f | 화면/부품 | 움직임 · 카메라 | 머묾 | 참조 |
|---|---|---|---|---|---|---|
| 1 | 0 | 90 | 글줄 `video-headline` "이번 달 미션" → "반복 업무를 줄이는 AI 자동화" | `motion-appear` → `motion-change` | `hold-beat` ×2 | R1 00:00 |
| 2 | 90 | 110 | `03-mission.png` 폰 | `motion-screen` → 따라 내리기 (제출 영역까지) | `hold-beat` | R2 00:03 |
| 3 | 200 | 90 | `mission-card.html` 2.8배 | `motion-appear` → 진행 바 채움 (motion.md 3장) | `hold-read` | R3 00:05 |
| 4 | 290 | 80 | `button-submit.html` `submit` | `motion-appear` → `motion-exit` | `hold-beat` | R5 00:13 |
| 5 | 370 | 110 | `04-approved.png` 폰 | 컷 → `hold-screen` → push-in 1.3배 (배지 쪽) | — | R4 00:07~00:10 |
| 6 | 480 | 45 | `badge-approved.html` 2.8배 + 글줄 "미션을 완성했어요!" | `motion-appear` · 글줄 강조 `duration-long` | `hold-beat` | R6 00:14 |
| 7 | 525 | 75 | 엔드 카드: `logo` white + `video-caption` | `motion-appear` | `hold-end` | R8 00:22 |

## B안 — 부품만 크게 (폰 짧게)
폰은 한 번만, 나머지는 부품을 떼어 차례로. 구도 R3 · R5가 중심.
- 글줄 → `mission-card` → `skill-card-1~3` `motion-list` → `button-submit` 문구 `submit`→`view-assets` `motion-change` → `badge-approved` → `04-approved` 폰 한 번 → 엔드
- 레퍼런스 반영: 구성 R1 · R3 · R5 · R6 · R7 · R8 (카메라 R4 없음)

## C안 — 폰 하나로 길게 (카메라 중심)
폰이 처음부터 끝까지 가운데. 카메라로 부분을 보여준다. 구도 R2 · R4가 중심.
- 글줄 → `03-mission` 폰 `motion-screen` → push-in 미션 카드 → 따라 내리기 제출 버튼 → 컷 `04-approved` → push-in 배지 → 엔드
- 레퍼런스 반영: 구성 R1 · R2 · R4 · R8 (부품 떼어내기 R3 · R5 없음)
