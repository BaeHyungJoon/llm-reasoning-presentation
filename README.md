# LLM은 어떻게 더 잘 생각하게 되었나

SSAFY AI 자기주도학습을 위한 24장짜리 Slidev 기술 발표 자료입니다.

발표는 다음 세 축으로 LLM reasoning의 발전을 설명합니다.

- Architecture Efficiency
- Reasoning-oriented Post-training / RL
- Adaptive Inference-time Compute / Agency

현재 24장 구성, 주요 시각 컴포넌트, speaker notes, 로컬 빌드까지 구현되어 있습니다. PDF/PPTX 등 최종 배포 산출물의 export QA는 아직 진행 전입니다.

## 1. 필요한 환경

### 필수

- Node.js `20.12.0` 이상
- pnpm
- Chromium 기반 브라우저

이 프로젝트에서 확인한 환경은 다음과 같습니다.

```text
Node.js  v24.18.0
pnpm     11.21.0
Slidev   52.19.0
```

Slidev 52.19.0이 요구하는 최소 Node.js 버전은 `20.12.0`입니다. 재현성을 위해 Node.js 20 LTS 이상과 pnpm 11 사용을 권장합니다.

pnpm이 설치되어 있지 않다면 다음 중 하나를 사용합니다.

```bash
npm install -g pnpm@11.21.0
```

또는 Corepack을 사용할 수 있는 Node.js 환경에서는 다음과 같이 활성화할 수 있습니다.

```bash
corepack enable
corepack prepare pnpm@11.21.0 --activate
```

### 권장 글꼴

슬라이드는 아래 순서로 한글 글꼴을 사용합니다.

1. Pretendard
2. Noto Sans KR
3. Apple SD Gothic Neo
4. Segoe UI

운영체제에 Pretendard 또는 Noto Sans KR을 설치하면 발표 환경 간 한글 줄바꿈과 자간 차이를 줄일 수 있습니다.

## 2. 프로젝트 설치

프로젝트 디렉터리에서 의존성을 설치합니다.

```bash
pnpm install
```

`playwright-chromium`은 Slidev의 PDF/PNG/PPTX export에 사용됩니다. `pnpm-workspace.yaml`에 해당 패키지의 설치 스크립트 실행이 허용되어 있으므로, 최초 설치 시 Chromium 다운로드가 함께 진행될 수 있습니다.

Windows PowerShell에서 `pnpm` 실행이 정책 문제로 차단되면 `pnpm.cmd`를 사용합니다.

```powershell
pnpm.cmd install
```

## 3. 개발 서버 실행

```bash
pnpm dev
```

기본적으로 Slidev 개발 서버가 실행되고 브라우저가 자동으로 열립니다. 자동으로 열리지 않으면 터미널에 표시된 주소로 접속합니다. 일반적인 기본 주소는 다음과 같습니다.

```text
http://localhost:3030
```

자동 브라우저 실행 없이 서버만 시작하려면 다음 명령을 사용할 수 있습니다.

```bash
pnpm exec slidev slides.md --port 3030
```

3030 포트가 사용 중이면 다른 포트를 지정합니다.

```bash
pnpm exec slidev slides.md --port 3031
```

개발 서버 실행 중 `slides.md`, `components/`, `styles/` 파일을 수정하면 화면에 자동 반영됩니다.

## 4. 발표 및 speaker notes

발표 화면에서 Slidev 단축키 `P`를 사용하면 presenter mode를 열 수 있습니다. Presenter mode에서는 `slides.md`에 작성된 speaker notes를 확인할 수 있습니다.

모든 슬라이드의 notes는 다음 구조를 사용합니다.

```text
Goal: 청중이 이해해야 할 핵심
Talk track: 자연스러운 설명을 위한 요약
Transition: 다음 슬라이드로 이어지는 문장
Source: 근거가 되는 로컬 문서 또는 논문
```

## 5. 프로덕션 빌드

```bash
pnpm build
```

빌드가 성공하면 정적 결과물이 `dist/`에 생성됩니다. 현재 프로젝트는 이 명령으로 24장 전체 빌드가 성공하는 상태입니다.

정적 결과물을 로컬에서 확인하려면 별도의 정적 서버를 사용하거나 Netlify/Vercel 설정을 이용할 수 있습니다.

## 6. Export 명령

기본 export 스크립트는 다음과 같습니다.

```bash
pnpm export
```

형식과 출력 파일을 직접 지정할 수도 있습니다.

```bash
pnpm exec slidev export slides.md --format pdf --output llm-reasoning-slides.pdf
pnpm exec slidev export slides.md --format png --output rendered-slides
pnpm exec slidev export slides.md --format pptx --output llm-reasoning-slides.pptx
```

> 현재 단계에서는 웹 빌드와 임시 화면 렌더만 검증했습니다. 최종 PDF/PPTX의 24페이지 수, 한글 글꼴, 수식, clipping 검증은 별도의 final export QA 단계에서 수행해야 합니다.

## 7. 주요 명령 요약

| 작업 | 명령 |
|---|---|
| 의존성 설치 | `pnpm install` |
| 개발 서버 | `pnpm dev` |
| 정적 빌드 | `pnpm build` |
| 기본 export | `pnpm export` |
| 포트 지정 실행 | `pnpm exec slidev slides.md --port 3031` |

Windows에서는 필요에 따라 `pnpm` 대신 `pnpm.cmd`를 사용할 수 있습니다.

## 8. 프로젝트 구조

```text
.
├─ slides.md                  # 24개 슬라이드와 speaker notes
├─ components/               # Vue/CSS 기반 커스텀 다이어그램
├─ styles/                   # 공통 theme, typography, layout, diagram 스타일
├─ docs/
│  ├─ presentation_brief.md  # 발표 범위와 핵심 thesis
│  ├─ slide_plan.md          # 슬라이드별 구현 명세
│  └─ sources.md             # 슬라이드별 claim-source mapping
├─ references/               # 발표의 근거가 되는 로컬 논문과 보고서
├─ assets/                   # 이미지 및 참고 시각 자료
├─ package.json              # 실행 스크립트와 의존성
├─ pnpm-lock.yaml            # 고정된 의존성 버전
└─ pnpm-workspace.yaml       # pnpm 및 Playwright 설치 설정
```

## 9. 콘텐츠를 수정할 때

프로젝트의 콘텐츠 우선순위는 다음과 같습니다.

1. `docs/presentation_brief.md`
2. `docs/slide_plan.md`
3. `references/`
4. `assets/reference_figures/`
5. 명시적으로 요청된 외부 조사

새로운 benchmark, 날짜, parameter count, optimizer, reward formulation 또는 모델 구조를 근거 없이 추가하지 마세요. 화면의 사실 주장을 변경했다면 `docs/sources.md`와 해당 슬라이드의 `Source` note도 함께 갱신해야 합니다.

Semantic color는 다음 규칙을 유지합니다.

- Architecture: cyan / blue
- Post-training / RL: violet / purple
- Inference-time Compute / Agency: amber / orange
- Baseline / neutral: white / gray

## 10. 문제 해결

### `pnpm` 명령을 찾을 수 없음

```bash
npm install -g pnpm@11.21.0
```

설치 후 새 터미널을 열고 `pnpm --version`을 확인합니다.

### Node.js 버전 오류

```bash
node --version
```

버전이 `20.12.0`보다 낮다면 Node.js 20 LTS 이상으로 업데이트합니다.

### Export 중 Chromium 오류

먼저 의존성을 다시 설치합니다.

```bash
pnpm install
```

브라우저 설치가 누락된 경우 다음 명령을 시도할 수 있습니다.

```bash
pnpm exec playwright install chromium
```

### 한글 줄바꿈이 다른 환경과 다름

발표에 사용하는 PC에도 Pretendard 또는 Noto Sans KR을 설치하고 브라우저를 다시 시작합니다. 최종 PDF export 전에는 반드시 실제 발표 PC 또는 동일한 글꼴 환경에서 페이지를 확인합니다.

### 화면이 잘리거나 비율이 다름

이 프로젝트는 `16:9`, `canvasWidth: 980` 기준입니다. 브라우저 zoom을 100%로 설정하고, projector가 16:9 출력을 사용하도록 확인합니다.
