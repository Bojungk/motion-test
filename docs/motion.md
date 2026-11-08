# motion.md

우리 서비스의 움직임 기준. 성격: **또렷한** — 짧게 들어오고, 넘치지 않고(오버슈트 없음), 정확히 멈춘다.
단위: 프레임(f), **30fps** 기준. 영상 렌더 fps가 다르면 ms 값을 기준으로 다시 환산한다.
규칙: 이 문서에 있는 값만 쓴다. 장면 순서 · 화면 배치는 여기 두지 않고 영상마다 비트 시트에 쓴다. 색 · 글자 · 로고는 `design.md`를 따른다.

출처 (시점 표기 `mm:ss`는 영상 A 기준)
- **영상 A**: Skillry · @SaadPastaDev `saadpastadev-347341` 원본 (24.56초, 1280×720, 30fps) → `references/saadpastadev-347341.mp4`. 프레임 차이 측정으로 움직임 길이를 셌다.
- **Carbon**: Carbon Design System — Motion overview (duration 6단계, productive/expressive 곡선)
- **Remotion**: Remotion Prompts — Apple-style device rise animation (30fps, 45f 상승, `Easing.out(Easing.cubic)`, 9f 간격)

---

## 1. Primitives

### Duration (6단계)

| 토큰 | f | ms | 출처 |
|---|---|---|---|
| `duration-instant` | 2 | 67 | Carbon `fast-01` 70ms · A 00:05 검색창 글자 입력 한 칸 1~2f |
| `duration-quick` | 4 | 133 | Carbon `fast-02` 110ms · A 00:16 "Buy" 줄 바뀜 4f · 00:20 마지막 줄 4f |
| `duration-short` | 6 | 200 | Carbon `moderate-01` 150ms · A 00:05 검색창 등장 5f · 00:14 체크 표시 6f · 00:17 회사명 한 줄 6f |
| `duration-medium` | 12 | 400 | Carbon `slow-01` 400ms · A 00:00 "is now" 글줄 바뀜 12f · 00:06 검색창→초록 알약 변형 11f |
| `duration-long` | 24 | 800 | Carbon `slow-02` 700ms(21f) · A 00:01 "instant" + 로고 퍼짐 24f · 00:15 알림 카드 내려옴 25f |
| `duration-slow` | 40 | 1333 | Remotion 기기 상승 45f · A 00:03 폰 화면 올라옴 40f · 00:09 차트로 밀고 들어감 38f |

### 곡선 (또렷한 → Carbon productive 계열, 오버슈트 없음)

| 토큰 | cubic-bezier | 출처 |
|---|---|---|
| `ease-standard` | `0.2, 0, 0.38, 0.9` | Carbon productive standard · A 00:09 카메라 밀기: 움직임이 가운데(00:09.7)에서 가장 크고 양끝이 느림 |
| `ease-enter` | `0, 0, 0.38, 0.9` | Carbon productive entrance · A 00:00 "is now": 첫 프레임이 가장 빠르고 12f 동안 줄어듦 |
| `ease-exit` | `0.2, 0, 1, 0.9` | Carbon productive exit · A 00:13 "to confirm buy" 밀기: 끝(00:13.9)으로 갈수록 빨라짐 |
| `ease-settle` | `0.33, 1, 0.68, 1` | Remotion `Easing.out(Easing.cubic)` · A 00:03 폰 상승: 40f 중 앞 10f에 대부분 이동, 뒤 30f 천천히 멈춤 |

- 스프링 · 바운스 곡선은 쓰지 않는다 (A 전체에서 되튐 없음, Remotion도 스프링 없음).
- Carbon expressive 곡선은 가져오지 않는다 (성격이 "또렷한"이라서).

### 간격 (stagger)

| 토큰 | f | 출처 |
|---|---|---|
| `stagger-step` | 8 | A 00:16~00:20 회사명 목록 8~9f마다 한 줄 · Remotion 알림 카드 9f 간격 |
| `stagger-type` | 4 | A 00:05 검색창 글자 4f마다 한 글자 (00:05.5 · 00:05.6 · 00:05.8) |

---

## 2. Semantic (5개)

Primitive를 직접 쓰지 않고 아래 이름으로 쓴다.

| 토큰 | duration | 곡선 | 언제 | 출처 |
|---|---|---|---|---|
| `motion-appear` | `duration-short` (6f) | `ease-enter` | 부품 하나가 화면에 나타남 | A 00:05 검색창 등장 5f · 00:14 체크 6f |
| `motion-change` | `duration-medium` (12f) | `ease-standard` | 같은 자리에서 상태 · 숫자 · 모양이 바뀜 | A 00:06 검색창→알약 11f · 00:00 글줄 바뀜 12f |
| `motion-exit` | `duration-quick` (4f) | `ease-exit` | 부품이 사라짐 (장면 끝은 컷, 5장) | A 00:16 "Buy" 줄 4f · 00:13 밀어서 확인 끝 |
| `motion-list` | `duration-short` (6f) + `stagger-step` (8f) | `ease-enter` | 같은 부품 여러 개가 차례로 들어옴 | A 00:17~00:20 회사명 줄 6f / 8f 간격 |
| `motion-screen` | `duration-slow` (40f) | `ease-settle` | 폰 화면(`src/screens`) 전체가 들어와 자리 잡음 | A 00:03 폰 상승 40f · Remotion 45f |

강조용 큰 움직임은 `duration-long` (24f) + `ease-enter`를 쓴다 (A 00:01 "instant" 24f, 00:15 알림 25f). 한 영상에 한두 번만.

---

## 3. Pattern (src/parts · src/screens)

| 대상 | 움직임 | Semantic | 출처 |
|---|---|---|---|
| `button-submit.html` | 문구 바뀜 (`data-state` 4개 사이) | `motion-change` | A 00:12 "to confirm buy" 버튼 상태 바뀜 |
| `button-submit.html` | 누름 → 다음 상태 | `motion-exit` 뒤 `motion-appear` | A 00:13 밀어서 확인 → 00:14 체크 |
| `badge-approved.html` | 등장 | `motion-appear` | A 00:14 체크 표시 6f |
| `mission-card.html` | 카드 등장 | `motion-appear` | A 00:05 검색창 등장 |
| `mission-card.html` | 진행 바 채움 | `duration-long` (24f) + `ease-standard` | A 00:01 강조 24f (2026-11-08 결정) |
| `stat-card.html` | 숫자 바뀜 | `motion-change` | A 00:11 금액 "50 → 5,000" 바뀜 |
| `skill-card-1~3.html` | 세 장 차례로 | `motion-list` | A 00:17 목록 8f 간격 |
| `asset-card.html` | 여러 장 차례로 · 상태 바뀜 | `motion-list` · `motion-change` | A 00:17 목록 · 00:12 상태 바뀜 |
| `brand-icon.html` · `logo.html` | 등장 | `motion-appear` (로고 자체는 움직이지 않음) | A 00:21 마지막 화면 등장 |
| `src/screens/*.png` | 폰 화면 들어옴 | `motion-screen` | A 00:03 · Remotion |
| `src/screens/*.png` | 화면 → 화면 | 컷 (5장) | A 00:07 · 00:10 · 00:14 화면 바뀜이 컷 |

시작값 (2026-11-08 결정)

| 토큰 | 값 | 출처 |
|---|---|---|
| `motion-appear` 시작 | 아래 16px (`space-content`) · 투명도 0 → 제자리 · 1 | A 00:05 검색창이 아래에서 올라옴 |
| `motion-screen` 시작 | 아래 400px · scale 0.9 → 제자리 · 1, 기울기 없음 | Remotion 400px에서 rotateX 빼고 scale 완화 |

---

## 4. 머무는 시간

움직임이 끝난 뒤 다음 움직임까지 화면이 멈춰 있는 시간.

| 토큰 | f | 언제 | 출처 |
|---|---|---|---|
| `hold-beat` | 15 | 글줄 · 작은 부품 하나 읽기 | A 00:01 "is now" 뒤 19f · 00:02 "instant" 뒤 14f |
| `hold-read` | 45 | 카드 하나 · 숫자 읽기 | A 00:10.8~00:12.4 키패드 화면 50f |
| `hold-screen` | 60 | 폰 화면 전체 살펴보기 | A 00:07.1~00:09.2 차트 화면 64f |
| `hold-end` | 75 | 영상 마지막 화면 | A 00:22.0~00:24.5 마지막 화면 약 75f |

- 움직임이 겹치지 않게 한다: 한 번에 한 부품만 움직이고, 앞 움직임이 끝나야 다음이 시작 (A 전체).

---

## 5. 카메라

| 항목 | 값 | 출처 |
|---|---|---|
| 밀어 들어가기 (push-in) | `duration-slow` (40f) + `ease-standard`, scale 1 → 1.3 | A 00:09.2~00:10.5 차트 쪽으로 38f, 약 1.3배 |
| 따라 내리기 (scroll) | `duration-slow` (40f) + `ease-settle` | A 00:03.3~00:04.7 검색 목록 내려감 |
| 장면 전환 | 컷 (페이드 · 디졸브 없음) | A 00:16.3 흰 화면 → 검은 화면 한 프레임 컷 |
| 흔들림 · 회전 | 쓰지 않음 | A 전체 |
