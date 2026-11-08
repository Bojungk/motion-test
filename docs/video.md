# video.md

영상 룩 기준. 캔버스 **16:9 · 1920×1080 · 30fps**.
규칙: 색 · 폰트는 `docs/design.md`에 있는 값만 쓴다. 움직임은 `docs/motion.md`를 따른다. 장면 순서 · 흐름 · 구성은 여기 두지 않는다 (레퍼런스와 비트 시트가 정함).
결정 (2026-11-08): 배경 **어두운** · 헤드라인 **단정하게** · 엔드 카드 **어두운**.

배율
- `video-type-scale` = **2.8** — 영상 글자 크기 = Figma 텍스트 스타일 값 × 2.8 (모션용 텍스트 배율). 크기 · 행간 모두 곱하고 정수로 반올림한다.
- 부품(`src/parts`)도 같은 2.8배로 키운다 → 부품 안 글자가 영상 글자 토큰과 같은 크기가 된다 (5장).

---

## 1. 텍스트 최소 크기

| 토큰 | px | 근거 |
|---|---|---|
| `video-text-min` | **31** | 가장 작은 스타일 `Text/eyebrow` 11 × 2.8 = 30.8 |

- 31px보다 작은 글자는 영상에 넣지 않는다. 부품 안 글자도 2.8배로 키우면 31px 이상이 된다.
- 어두운 바탕에서 `video-text-muted`(#75777c)는 39px(`video-label`) 이상에서만 쓴다. 그보다 작은 글자는 `video-text`.

---

## 2. 배경

| 토큰 | hex | design.md 변수 | 쓰는 곳 |
|---|---|---|---|
| `video-bg` | `#18191b` | `color-text` | 영상 기본 바탕 (어두운) |
| `video-bg-raised` | `#000000` | `color-illustration-000000` | 바탕 위 한 단 깊은 면 (폰 테두리 뒤 등) |
| `video-end-bg` | `#18191b` | `color-text` | 엔드 카드 바탕 (어두운, 기본 바탕과 같음) |

- 바탕은 단색. 그라데이션 · 질감 · 무늬 없음 (design.md에 없음).
- 브랜드 파랑 `color-primary`(#3759de)는 바탕 전체에 깔지 않는다. 버튼 · 진행 바처럼 부품 안에서만 보인다.
- 엔드 카드 로고는 흰 버전: `src/assets/logo-logotype-white.svg` · `logo-symbol-white.svg`.

---

## 3. 글자

폰트: `Pretendard` 400 · 600 · 700, `src/assets/fonts/`의 로컬 파일 (design.md 3장 A). 첫 프레임 캡처 전에 `document.fonts.ready`를 기다린다. 자간 0.

### 색

| 토큰 | hex | design.md 변수 |
|---|---|---|
| `video-text` | `#ffffff` | `color-bg` |
| `video-text-muted` | `#75777c` | `color-text-muted` |
| `video-text-accent` | `#edf1ff` | `color-primary-subtle` (어두운 바탕에서 강조할 단어) |

### 크기 (Figma × 2.8)

| 토큰 | Figma 스타일 | 굵기 | 크기 px | 행간 px |
|---|---|---|---|---|
| `video-headline` | `Text/display` 28 / 34 | 700 | 78 | 95 |
| `video-title` | `Text/title` 24 / 32 | 600 | 67 | 90 |
| `video-subtitle` | `Text/compact-title` 22 / 28 | 700 | 62 | 78 |
| `video-section` | `Text/section` 20 / 28 | 700 | 56 | 78 |
| `video-heading` | `Text/heading` 18 / 28 | 600 | 50 | 78 |
| `video-body` | `Text/body` 15 / 24 | 400 | 42 | 67 |
| `video-list` | `Text/list-title` 15 / 22 | 600 | 42 | 62 |
| `video-label` | `Text/label` 14 / 20 | 600 | 39 | 56 |
| `video-caption` | `Text/caption` 12 / 16 | 400 | 34 | 45 |
| `video-eyebrow` | `Text/eyebrow` 11 / 16 | 600 | 31 | 45 |

- 헤드라인은 **단정하게**: `video-headline` 78px가 가장 큰 글자. 이보다 큰 크기는 만들지 않는다.
- 한 글줄은 한 줄로. 줄바꿈이 필요하면 행간 토큰 그대로.

---

## 4. 폰 프레임

`src/screens/*.png`(780×1688 = 390×844 @2x)를 폰 화면으로 보여줄 때.
design.md에 폰 프레임(베젤 · 모서리) 값이 **없음** → 베젤을 그리지 않고 화면 이미지만 둥글게 잘라 쓴다.

| 토큰 | 값 | 근거 |
|---|---|---|
| `video-phone-scale` | 1.1 → 화면 429×928 px | 1080 높이 안에 위아래 76px씩 남김 |
| `video-phone-radius` | 13 px | `radius-card` 12 × 1.1 |
| `video-phone-edge` | 1px 선 `#75777c` (`color-text-muted`) | 어두운 바탕에서 흰 화면 가장자리 구분 |
| `video-phone-shadow` | 0 · 9 · 흐림 26 · `#0000001F` | `Shadow/lg` × 1.1 |

- 카메라로 밀어 들어갈 때(motion.md 5장, 1.3배)는 화면 이미지를 그대로 키운다. 다시 그리지 않는다.
- 화면 이미지 안의 글자 · 색은 고치지 않는다.

---

## 5. parts

`src/parts/*.html`을 영상에 올릴 때.

| 토큰 | 값 | 근거 |
|---|---|---|
| `video-part-scale` | 2.8 | `video-type-scale`과 같음 → 부품 글자 = 3장 글자 크기 |
| `video-part-shadow` | 0 · 11 · 흐림 34 · `#00000014` | `Shadow/md` × 2.8 |

2.8배 크기 (원본 → 영상)

| 부품 | 원본 | 영상 px |
|---|---|---|
| `asset-card` | 350×74 | 980×207 |
| `badge-approved` | 108×32 | 302×90 |
| `brand-icon` | 98×98 | 274×274 |
| `button-submit` | 350×44 | 980×123 |
| `logo` (logotype) | 149×19 | 417×53 |
| `logo` (symbol) | 100×100 | 280×280 |
| `mission-card` | 350×253 | 980×708 |
| `skill-card-1~3` | 350×88 | 980×246 |
| `stat-card` | 350×101 | 980×283 |

- 부품 안의 색 · 간격 · 모서리는 HTML 그대로 두고 통째로 `scale(2.8)`. 부품을 영상용으로 다시 만들지 않는다.
- 부품의 흰 바탕(`color-bg`)은 어두운 `video-bg` 위에서 그대로 카드로 보인다. 테두리를 더하지 않는다.
- `mission-card`(높이 708)는 화면 높이의 2/3 가까이 차지한다. 다른 부품과 같은 화면에 겹쳐 놓을지는 비트 시트에서 정한다.
