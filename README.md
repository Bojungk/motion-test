# motion-test — 허들링 모션 하네스

허들링 클럽 서비스 화면으로 **일관된 기준의 모션 영상**을 만드는 실습 저장소예요.
기준 문서(`docs/`)와 화면 · 부품(`src/`)은 고정하고, 영상마다 바뀌는 건 BRIEF와 레퍼런스뿐이에요.
영상은 [HyperFrames](https://hyperframes.heygen.com)(HTML → 영상)로 만들어요.

## 결과물

| 버전 | 길이 | 파일 | 내용 |
|---|---|---|---|
| v1 | 20초 | `out/mission-approved/video/renders/mission-approved.mp4` | 장면표 A안, 소리 없음 |
| v2 | 15초 | `out/mission-approved/video/renders/mission-approved-15s.mp4` | 120BPM 박자 컷 · 효과음 10개 · 타이핑 · 카메라 밀기 2번 |
| v3 | 15초 | `out/mission-approved/video-v3/renders/mission-approved-v3-15s.mp4` | v2 + 장면마다 이미지 옆 타이포 · 숫자 카운트업 · 효과음 13개 |

## 폴더 구조

```
CLAUDE.md                  하네스 규칙 (바뀌는 것 / 고정된 것, 역할, 승인, 결과 위치)
.claude/
  agents/                  art-director · director · builder · critic
  skills/make-video/       "모션 만들자"로 시작하는 영상 한 편 순서
docs/
  design.md                색 · 글자 · 간격 · 부품 목록 (Figma에서 읽은 값)
  motion.md                움직임 기준: 길이 6단계 · 곡선 4개 · Semantic 5개 · 머무는 시간 · 카메라
  video.md                 영상 룩: 1920×1080 · 30fps · 어두운 배경 · 글자 ×2.8 · 폰 프레임 · 부품 배율
src/
  parts/                   HTML 부품 (카드 · 버튼 · 배지 · 로고 …)
  screens/                 앱 화면 이미지 5장
  assets/                  캐릭터 · 로고 · Pretendard 폰트
references/                레퍼런스 영상
out/<영상이름>/            영상마다 BRIEF · refs · 장면표 · 스냅보드 · HyperFrames 프로젝트 · 판정 기록
```

## 영상 만드는 순서

Claude Code에서 **"모션 만들자"**라고 하면 `make-video` 스킬이 아래 순서로 진행해요.

1. **BRIEF**: 무엇을 · 몇 초 · 레퍼런스, 세 가지를 물어요.
2. **레퍼런스 정리** (art-director): 구성 · 구도 · 카메라 · 전환 · 글자 배치만 우리 토큰으로 옮겨요.
3. **장면표** (director): 3안 중에서 고르기 → **승인 1**
4. **스냅보드** (builder → critic 판정) → **승인 2**
5. **영상** (builder → critic 판정) → 렌더

critic은 세 가지만 세요: docs에 없는 숫자 0개 · 화면에 없는 UI 0개 · 레퍼런스 반영 60% 이상.

## 직접 미리보기 · 렌더

FFmpeg가 필요해요 (Windows: `winget install --id Gyan.FFmpeg -e`).

```bash
cd out/mission-approved/video-v3
npx hyperframes preview      # 브라우저 Studio 미리보기
npx hyperframes check        # 검사
npx hyperframes render -q delivery -o renders/out.mp4
```

## Figma

`docs/motion.md`의 값은 Figma 파일에 변수로도 등록했어요.

- **Motion Primitives** (16개): `duration/*` · `stagger/*` (TIMING, 초) · `easing/*` (EASING) · `distance/*` · `scale/*` (숫자)
- **Motion Semantic** (14개): `motion-appear` · `change` · `exit` · `list` · `screen`의 속성별 별칭
- 15초 v2 영상은 `Motion · mission-approved 15s` 프레임에 키프레임으로 옮겼어요. 소리는 빠져 있어요.

## 출처 · 라이선스

- **움직임 값:** Carbon Design System — Motion overview, Remotion — Apple-style device rise animation
- **레퍼런스 영상:** `references/saadpastadev-347341.mp4`는 Skillry에 올라온 @SaadPastaDev의 영상이에요. 참고용이라 저장소를 공개할 때는 빼야 해요.
- **효과음:** Openverse(Freesound)에서 받은 CC0 · CC BY 효과음이에요. CC BY 3개의 출처는 `out/mission-approved/*/assets/sfx/CREDITS.md`에 있고, 영상을 올릴 때 함께 적어야 해요.
- **화면 · 부품 · 디자인 문서:** 원본 저장소 `figmatutor-info/huddling-motion-start`에서 가져왔어요.
