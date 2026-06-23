# Stauffer & Grimson 30분 발표 PPT 구성안

대상 논문: Chris Stauffer, W. E. L. Grimson, *Adaptive Background Mixture Models for Real-Time Tracking*  
발표 정보: 2026.06.24, 박천웅, IRV-Lab  
목표: 30분 세미나 발표용 슬라이드 구성안, 구체 디자인 명세, 발표자 스크립트 작성  
작업 기준: `agent.md`의 1280x720 HTML/CSS 슬라이드 생성 방식과 연설문 작성 방식을 따른다.

## 0. 제작 원칙

### 소스 사용 원칙

- `agent.md`: 슬라이드 제작 방법론. 16:9, 1280x720, Tailwind CSS, Font Awesome, Noto Sans KR, 텍스트 공백 정규화, 코드 블록 공백 관리 기준으로 사용한다.
- `stauffer_grimson_seminar_points_ko.md`: 발표 흐름의 1차 뼈대.
- `adaptive_background_mixture_models_analysis_ko.md`: 수식, 파라미터, 결과, 한계, 예상 질문 보강.
- `Adaptive_background_mixture_models_for_real-time_tracking.pdf`: 논문 원문 근거 확인용.
- `seminar_problem_timeline.svg`, `seminar_gmm_intuition.svg`, `seminar_method_pipeline.svg`: 직접 삽입하지 않는다. 일부 깨짐이 있으므로 정보 구조와 색감만 참고하여 슬라이드 내부 도형, 텍스트, 아이콘으로 다시 그린다.

### 디자인 시스템

- 슬라이드 크기: 1280x720.
- 기본 폰트: `Noto Sans KR`, 보조로 `Arial`, `sans-serif`.
- 배경색: `#f7f4ef` 또는 `#f6f2ea`.
- 기본 텍스트: `#1d2b2f`.
- 보조 텍스트: `#52646b`.
- 메인 강조: `#2f7568`.
- 어두운 강조 블록: `#1f2f35`.
- 위험/한계 강조: `#a64235`.
- 보조 강조: `#d8a24b`.
- 경계선: `#d8cdb7`.
- 카드 반경: 8px 이하. 카드 안에 카드를 중첩하지 않는다.
- 1장은 반드시 제목 슬라이드로 두고, 논문 제목, 저자, 발표 날짜, 발표자, 소속을 명확히 배치한다.
- 제목은 좌상단 고정, 본문은 2열 또는 3열 grid로 구성한다.
- 중요한 한 문장은 어두운 하단 밴드 또는 좌측 statement block에 넣는다.
- SVG의 깨진 텍스트나 선을 그대로 쓰지 않고, 핵심 구조만 HTML/CSS 도형과 Font Awesome 아이콘으로 재작성한다.

### HTML/CSS 구현 메모

```html
<link href="https://cdn.jsdelivr.net/npm/tailwindcss@2.2.19/dist/tailwind.min.css" rel="stylesheet">
<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/@fortawesome/fontawesome-free@6.4.0/css/all.min.css">
<link href="https://fonts.googleapis.com/css2?family=Noto+Sans+KR:wght@300;400;500;700;800&display=swap" rel="stylesheet">
<style>
.slide {
  width: 1280px;
  height: 720px;
  font-family: 'Noto Sans KR', Arial, sans-serif;
  background: #f7f4ef;
  color: #1d2b2f;
}
</style>
```

코드 블록이나 수식 블록은 `<pre><code>` 안쪽 첫 줄이 불필요한 공백으로 시작하지 않도록 작성한다.

```html
<div class="bg-gray-900 text-white p-4 rounded">
<pre><code>P(Xt) = sum_i^K w_i,t * eta(Xt, mu_i,t, Sigma_i,t)
Sigma_k,t = sigma_k,t^2 * I</code></pre>
</div>
```

## 1. 전체 시간 배분

| 구간 | 슬라이드 | 시간 | 목적 |
| --- | --- | ---: | --- |
| 발표 정보와 도입 | 1-5 | 7.1분 | 제목, 발표자 정보, 문제를 배경 제거가 아니라 배경 기억의 문제로 재정의 |
| 기존 한계와 핵심 전환 | 6-7 | 4.3분 | 단일 배경 가정에서 다중 상태 배경으로 이동 |
| 방법 설명 | 8-12 | 11.0분 | GMM, online update, background selection, pipeline, parameter 해석 |
| 결과와 평가 | 13-15 | 6.3분 | 왜 작동했는지, 어떤 근거가 있는지, 어디서 실패하는지 설명 |
| 계보와 마무리 | 16 | 1.3분 | 현대적 의미와 핵심 메시지 정리 |

총 발표 시간: 30분.

## 2. 슬라이드별 구성안

### Slide 1. 제목: 논문 및 발표자 정보

발표 시간: 0.9분

핵심 메시지: 발표 논문, 저자, 발표자, 소속, 날짜를 명확히 알리고 세미나의 공식 시작점을 만든다.

화면 구성:
- 좌측 65%: 논문 제목을 가장 크게 배치하고, 그 아래 저자명을 둔다.
- 우측 35%: 발표자 정보 패널. 발표자, 소속, 발표 날짜를 세 줄로 정리한다.
- 배경에는 아주 옅은 픽셀 grid와 Gaussian cluster motif를 CSS 도형으로 배치한다.

구체 디자인:
- 배경은 `#f7f4ef`.
- 논문 제목은 46px, weight 800, `#1d2b2f`, 줄 간격은 1.1.
- 저자명은 22px, `#52646b`.
- 발표자 정보는 어두운 패널 `#1f2f35`에 흰색 텍스트로 배치한다.
- 발표자 이름 `박천웅`은 30px, 소속 `IRV-Lab`과 날짜 `2026.06.24`는 22px.
- Font Awesome 아이콘: `fa-file-lines`, `fa-user`, `fa-building-columns`, `fa-calendar-days`.

본문 텍스트:
- Adaptive Background Mixture Models for Real-Time Tracking
- Chris Stauffer & W. E. L. Grimson
- 발표자: 박천웅
- 소속: IRV-Lab
- 발표 날짜: 2026.06.24

발표자 스크립트:
> 안녕하세요. 오늘 발표할 논문은 Chris Stauffer와 W. E. L. Grimson의 Adaptive Background Mixture Models for Real-Time Tracking입니다. 발표자는 IRV-Lab의 박천웅이고, 발표일은 2026년 6월 24일입니다. 이 논문은 고정 카메라 영상에서 배경과 전경을 어떻게 안정적으로 분리할 것인가를 다룬 고전적인 background modeling 논문입니다.

전환 문장:
> 본격적으로 내용에 들어가기 전에, 이 논문의 핵심 관점을 한 문장으로 먼저 잡겠습니다.

### Slide 2. 핵심 관점: 배경은 한 장의 이미지가 아니다

발표 시간: 0.8분

핵심 메시지: 이 논문의 중심은 foreground detection 자체보다, 시간 속에서 변하는 배경을 어떻게 기억하고 갱신할 것인가에 있다.

화면 구성:
- 좌측 60%: 발표 핵심 문장과 오늘의 질문.
- 우측 40%: CSS로 만든 픽셀 그리드. 일부 픽셀은 청록, 황토, 벽돌색으로 천천히 번지는 듯한 분포 느낌을 준다.
- 하단 작은 statement line: background subtraction -> online background modeling.

구체 디자인:
- 배경은 `#f7f4ef`.
- 제목은 44px, weight 800, `#1d2b2f`.
- 핵심 문장은 28px, `#2f7568`.
- 우측 픽셀 그리드는 12x8 작은 사각형을 grid로 배치하고 opacity를 다르게 준다.
- Font Awesome 아이콘: `fa-video`, `fa-layer-group`.

본문 텍스트:
- 배경은 한 장의 고정 이미지가 아니라, 각 픽셀이 시간 속에서 반복해서 보이는 여러 상태의 집합이다.
- 질문: 변화하는 현실 배경을 계속 학습하면서 새 객체만 전경으로 분리할 수 있는가?
- 관점 전환: background subtraction -> online background modeling.

발표자 스크립트:
> 이 논문을 한 문장으로 요약하면, 배경을 한 장의 이미지로 보지 말고 시간 속에서 학습되는 분포로 보자는 제안입니다. 발표에서는 수식을 먼저 설명하기보다, 왜 이런 관점 전환이 필요했는지, 그리고 그 전환이 어떤 알고리즘 구조로 이어졌는지를 중심으로 보겠습니다.

전환 문장:
> 먼저 가장 단순한 배경 제거가 왜 현실 영상에서 깨지는지부터 보겠습니다.

### Slide 3. 직관적 출발점: 현재 프레임에서 배경을 빼면 되는가

발표 시간: 1.7분

핵심 메시지: 전통적 background subtraction은 직관적이지만, 현실에서는 배경 자체가 계속 변한다.

화면 구성:
- 3단 수식형 흐름: 현재 프레임 - 배경 이미지 = 전경 마스크.
- 오른쪽에는 실패 요인 4개를 작은 아이콘과 함께 배치.
- `seminar_problem_timeline.svg`의 문제 제기 부분을 재구성하되 직접 삽입하지 않는다.

구체 디자인:
- 중앙에 큰 가로 파이프라인. 각 박스는 240x150.
- 박스 사이에는 Font Awesome `fa-minus`, `fa-equals` 아이콘 사용.
- 실패 요인은 우측 세로 리스트: 조명 변화, 흔들리는 나뭇잎, 그림자/반사, 정지한 전경.
- 실패 요인 텍스트는 22px 이하로 줄여 한 줄에 들어가게 한다.

본문 텍스트:
- 단순한 생각: 현재 프레임 - 배경 이미지 = 움직이는 물체
- 하지만 현실에서는 배경 이미지가 안정적으로 존재하지 않는다.
- 조명, 그림자, 물결, 나뭇잎, 반사, 정지 객체가 모두 판단을 흔든다.

발표자 스크립트:
> 배경 제거의 가장 단순한 형태는 현재 프레임에서 미리 저장한 배경 이미지를 빼는 것입니다. 차이가 크면 전경, 차이가 작으면 배경이라고 판단합니다. 이 방식은 실험실처럼 장면이 통제되어 있으면 이해하기 쉽고 빠릅니다. 하지만 실제 감시 영상에서는 배경이라고 부르는 대상이 계속 변합니다. 햇빛은 이동하고, 그림자는 생기고 사라지고, 나무나 물결은 배경이지만 계속 움직입니다. 그래서 논문은 단순히 움직임을 찾는 문제가 아니라, 무엇을 배경으로 기억할지의 문제로 출발합니다.

전환 문장:
> 이 문제가 특히 중요해진 배경에는 1990년대 말의 실시간 영상 처리 환경이 있습니다.

### Slide 4. 시대적 압력: 장시간 실시간 감시 시스템

발표 시간: 1.7분

핵심 메시지: 계산 성능이 올라가면서 짧은 실험 영상이 아니라 장기간 실외 운용을 견디는 background model이 필요해졌다.

화면 구성:
- 좌측: 1990s real-time vision이라는 짧은 timeline.
- 우측: 실시간, 장시간, 실외, 무인 적응이라는 네 개의 조건.
- 하단 statement band.

구체 디자인:
- timeline은 4개의 노드로 단순화: short clips, fixed background, outdoor cameras, adaptive model.
- 각 조건은 둥근 태그가 아니라 작은 사각 패널로 배치한다.
- 배경은 밝게, 하단 밴드는 `#1f2f35`.

본문 텍스트:
- 실시간 처리가 가능해지자 연구 문제는 더 어려워졌다.
- 짧은 영상이 아니라 날씨와 시간 변화가 있는 장면을 오래 처리해야 한다.
- 필요한 조건: real-time, long-term, outdoor, unsupervised adaptation.

발표자 스크립트:
> 이 논문이 나온 시점에는 실시간 영상 처리가 연구실 수준을 넘어 실제 감시 시스템의 형태로 가능해지고 있었습니다. 그러면 더 이상 짧고 깨끗한 영상만 보면 안 됩니다. 카메라는 하루 종일, 몇 달 동안 돌아가고, 장면은 실외일 수 있으며, 사람의 재초기화 없이 계속 적응해야 합니다. 이 논문이 중요해지는 지점은 바로 여기에 있습니다. 배경 모델은 처음 한 번 만드는 것이 아니라, 계속 유지되는 시스템의 일부가 되어야 합니다.

전환 문장:
> 그래서 논문이 실제로 던지는 질문은 다음과 같이 정리할 수 있습니다.

### Slide 5. 문제 정의: 시스템은 무엇을 배경으로 기억해야 하는가

발표 시간: 2.0분

핵심 메시지: 핵심 문제는 foreground pixel을 찾는 것이 아니라, 시간적으로 변하는 정상 상태를 배경으로 학습하는 것이다.

화면 구성:
- 중앙에 큰 질문: "무엇을 배경으로 기억해야 하는가?"
- 주변에 5개 상황 카드: illumination, repetitive motion, shadow/reflection, stopped object, reappearing background.
- 하단에 발표 전체 thesis.

구체 디자인:
- 중앙 질문은 40px, `#1d2b2f`.
- 상황 카드는 180x95, 아이콘 + 두 줄 설명.
- 하단 thesis는 어두운 밴드에 흰색 텍스트.
- SVG를 쓰지 않고 HTML grid로 재작성.

본문 텍스트:
- 같은 픽셀은 시간에 따라 여러 정상값을 가질 수 있다.
- 배경은 고정 이미지가 아니라 반복적으로 관측되는 상태들의 모델이다.
- 발표 thesis: background subtraction -> online background modeling.

발표자 스크립트:
> 여기서 핵심 질문은 "움직이는 물체가 어디인가"보다 한 단계 앞에 있습니다. 시스템은 무엇을 배경으로 기억해야 할까요? 같은 픽셀이라도 시간에 따라 여러 값을 가질 수 있습니다. 도로 픽셀은 대부분 회색이지만, 그림자 아래에서는 어두워지고, 반사 때문에 밝아질 수도 있습니다. 그 값들이 반복적이고 안정적이라면 전경이 아니라 배경의 일부일 수 있습니다. 이 논문은 배경 제거를 온라인 배경 모델링 문제로 바꿉니다.

전환 문장:
> 이 전환이 왜 필요한지, 기존 접근들의 한계를 먼저 비교하겠습니다.

### Slide 6. 기존 접근의 한계

발표 시간: 2.0분

핵심 메시지: 초기 배경, 시간 평균, 단일 Gaussian은 각각 단순하지만 다봉 배경과 장기 변화에 한계가 있다.

화면 구성:
- 3열 비교표.
- 각 열: 방식, 장점, 깨지는 지점, 발표용 한 줄 평가.

구체 디자인:
- 표를 일반 표처럼 빽빽하게 만들지 않고, 3개의 세로 패널로 배치.
- 패널 상단 아이콘:
  - 초기 배경: `fa-image`
  - 시간 평균: `fa-clock-rotate-left`
  - 단일 Gaussian: `fa-chart-simple`
- 한계 문장은 벽돌색 `#a64235`.

본문 텍스트:
- 초기 배경 저장: 단순하지만 장면 변화에 취약.
- 시간 평균: 천천히 적응하지만 느린 물체와 반복 배경에 약함.
- 단일 Gaussian: 픽셀별 threshold가 가능하지만 여러 정상 상태를 설명하지 못함.

발표자 스크립트:
> 기존 방법을 세 가지로 단순화해 볼 수 있습니다. 첫째, 처음 배경을 저장해 두는 방식은 빠르고 쉽지만 시간이 지나면 틀어집니다. 둘째, 시간 평균은 어느 정도 적응하지만, 느린 물체가 평균에 섞이거나 반복적으로 움직이는 배경을 흐리게 만듭니다. 셋째, 단일 Gaussian은 픽셀마다 평균과 분산을 둔다는 점에서 발전했지만, 한 픽셀이 여러 정상 상태를 갖는 상황을 설명하지 못합니다. 이 마지막 문제가 이 논문의 직접적인 출발점입니다.

전환 문장:
> 그래서 논문은 한 픽셀에 하나의 배경값만 두는 가정을 버립니다.

### Slide 7. 핵심 아이디어: 한 픽셀이 여러 정상값을 기억한다

발표 시간: 2.3분

핵심 메시지: Gaussian mixture는 한 픽셀에 가능한 색 후보를 여러 개 저장하는 방식이다.

화면 구성:
- 좌측: 한 픽셀의 시간 축 관측값. 작은 색 점들이 시간 순서로 이어짐.
- 중앙: 점들이 세 개의 cluster로 모이는 그림.
- 우측: "배경 후보 A", "배경 후보 B", "전경 후보" 목록.
- `seminar_gmm_intuition.svg`는 직접 사용하지 않고 구조만 재구성한다.

구체 디자인:
- 좌측 시간 축은 얇은 선과 12개 색 점.
- 중앙 cluster는 반투명 ellipse 3개. 색상은 청록, 황토, 벽돌색.
- 우측 목록은 카드 대신 border-left 강조 블록.
- 핵심 문장은 하단 밴드에 배치.

본문 텍스트:
- Gaussian 하나 = 이 픽셀에서 자주 보였던 색의 덩어리.
- Mixture = 그런 덩어리 여러 개의 목록.
- 자주 보이고 안정적인 덩어리 = 배경 후보.
- 드물거나 넓게 흩어지는 덩어리 = 전경 후보.

발표자 스크립트:
> 이 논문의 직관은 간단합니다. 픽셀 하나를 작은 관찰자로 보면 됩니다. 이 픽셀은 매 프레임마다 색 값을 하나씩 봅니다. 충분히 오래 보면 값들이 아무렇게나 흩어지는 것이 아니라 몇 개의 덩어리로 모일 수 있습니다. 예를 들어 대부분은 도로 색, 가끔은 그림자 색, 드물게는 지나가는 자동차 색이 될 수 있습니다. Gaussian 하나는 이런 색의 덩어리이고, Gaussian mixture는 그 덩어리 여러 개를 동시에 기억하는 방식입니다.

전환 문장:
> 이제 이 직관을 논문이 어떤 수식으로 표현했는지 보겠습니다.

### Slide 8. 모델: 픽셀값의 확률을 Gaussian mixture로 본다

발표 시간: 2.8분

핵심 메시지: 현재 픽셀값은 K개의 Gaussian component가 섞인 확률분포에서 나온 것으로 모델링된다.

화면 구성:
- 좌측 55%: 수식 블록.
- 우측 45%: 변수 해석 카드 4개.
- 하단: full covariance 대신 `sigma^2 I`를 쓰는 이유.

구체 디자인:
- 수식 블록은 어두운 코드 블록처럼 보이게 하되, 코드가 아니라 equation panel로 명명.
- 변수 해석:
  - `K`: 기억할 후보 수
  - `w`: 후보의 빈도
  - `mu`: 후보의 중심 색
  - `sigma`: 후보의 흔들림
- 수식은 너무 작아지지 않게 24px monospace.

본문 텍스트:
```text
P(Xt) = sum_i^K w_i,t * eta(Xt, mu_i,t, Sigma_i,t)
Sigma_k,t = sigma_k,t^2 * I
```

- `Xt`: 현재 픽셀값.
- `K`: mixture component 수. 논문에서는 계산량에 따라 보통 3-5 정도.
- 계산량을 줄이기 위해 RGB full covariance 대신 isotropic covariance를 사용한다.

발표자 스크립트:
> 수식으로 쓰면 현재 픽셀값 Xt가 관측될 확률을 K개의 Gaussian이 섞인 형태로 둡니다. 여기서 weight는 그 후보가 얼마나 자주 나타났는지, 평균은 그 색 덩어리의 중심, 분산은 값이 얼마나 흔들리는지를 의미합니다. 중요한 점은 이 모델이 픽셀마다 따로 존재한다는 것입니다. 모든 픽셀이 자기만의 작은 mixture model을 가지고 있는 셈입니다. 다만 실시간 처리가 중요하기 때문에 full covariance를 쓰지 않고, 계산이 쉬운 sigma squared I 형태로 단순화합니다.

전환 문장:
> 모델을 세웠다면, 다음 문제는 매 프레임마다 이 모델을 어떻게 갱신하느냐입니다.

### Slide 9. 온라인 업데이트: 판단과 학습이 동시에 일어난다

발표 시간: 2.2분

핵심 메시지: 새 픽셀값은 기존 component와 match되는지 검사되고, match 여부에 따라 weight, mean, variance가 온라인으로 갱신된다.

화면 구성:
- 상단: 5단 decision flow.
- 하단 좌측: weight update 식.
- 하단 우측: match/no match의 의미.

구체 디자인:
- flow는 박스 5개: input, match check, update matched, replace weakest, normalize.
- match check에는 `2.5 sigma` 배지를 붙인다.
- 수식은 두 줄만 사용해서 과밀하지 않게 한다.

본문 텍스트:
```text
w_k,t = (1 - alpha) * w_k,t-1 + alpha * M_k,t
rho = alpha * eta(Xt | mu_k, sigma_k)
```

- match: 기존 평균에서 `2.5 sigma` 이내.
- match된 component: 평균과 분산 갱신.
- match되지 않은 component: weight 감소.
- 아무 component도 match되지 않으면 가장 약한 component를 새 값 중심으로 교체.

발표자 스크립트:
> 매 프레임에서 픽셀값이 들어오면, 먼저 기존 Gaussian 중 하나와 충분히 가까운지 봅니다. 논문에서는 평균에서 2.5 sigma 이내이면 match로 봅니다. match가 있으면 그 component의 평균과 분산을 조금 갱신하고 weight를 올립니다. 나머지 component는 상대적으로 weight가 줄어듭니다. 아무것도 match되지 않으면 가장 덜 중요한 component를 현재 픽셀값 중심의 새 component로 바꿉니다. 그래서 이 알고리즘은 현재 프레임을 분류하면서 동시에 다음 프레임의 배경 기억을 수정합니다.

전환 문장:
> 하지만 mixture 안에 있는 모든 component가 배경은 아닙니다. 어떤 component를 배경으로 볼지 정해야 합니다.

### Slide 10. 배경 선택: 자주 보이고 안정적인 component부터

발표 시간: 2.2분

핵심 메시지: 논문은 `w / sigma`로 component를 정렬하고, 누적 weight가 `T`를 넘을 때까지 배경으로 선택한다.

화면 구성:
- 좌측: 세 component를 `w / sigma` 기준으로 정렬한 막대.
- 중앙: 누적 weight가 threshold `T`를 넘는 지점 표시.
- 우측: 배경/전경 판단 규칙.

구체 디자인:
- 정렬 막대는 가로 bar 3개. width는 weight, height 또는 흐림은 sigma 느낌.
- threshold `T`는 세로 선으로 표시.
- 배경으로 선택된 bar는 청록, 제외된 bar는 벽돌색.

본문 텍스트:
```text
score_k = w_k / sigma_k
B = argmin_b (sum_k=1^b w_k > T)
```

- `w`: 많이 관측되었는가.
- `sigma`: 안정적인가.
- `T`: 최근 데이터 중 배경이 설명해야 하는 최소 비율.

발표자 스크립트:
> mixture 안에 component가 여러 개 있어도 모두 배경으로 인정하면 안 됩니다. 지나가는 자동차 색도 잠깐 component가 될 수 있기 때문입니다. 논문은 component를 w 나누기 sigma 기준으로 정렬합니다. 자주 보였고, 동시에 안정적인 component일수록 위로 올라갑니다. 그 다음 누적 weight가 threshold T를 넘을 때까지 상위 component를 배경으로 선택합니다. 현재 픽셀값이 이 배경 component 중 하나에 match되면 배경, 아니면 전경입니다.

전환 문장:
> 이 픽셀 단위 판단이 전체 영상 처리 파이프라인에서는 이렇게 연결됩니다.

### Slide 11. 전체 파이프라인: pixel model에서 tracking까지

발표 시간: 2.0분

핵심 메시지: 논문의 핵심은 background modeling이고, tracking은 foreground mask를 실제 시스템으로 연결하는 후처리 단계다.

화면 구성:
- `seminar_method_pipeline.svg`를 직접 쓰지 않고 새로 그린 6단 파이프라인.
- 단계: frame input -> pixel mixture -> background selection -> foreground mask -> connected components -> tracking.
- 각 단계마다 한 줄 설명.

구체 디자인:
- 6개 단계는 가로로 배치하되 마지막 tracking은 좁게 만들지 말고 160px 이상 확보한다.
- 각 단계는 아이콘 중심:
  - frame: `fa-film`
  - mixture: `fa-layer-group`
  - selection: `fa-filter`
  - mask: `fa-table-cells`
  - components: `fa-object-group`
  - tracking: `fa-location-crosshairs`
- 하단 dark band에 핵심 문장.

본문 텍스트:
- 매 프레임에서 모든 픽셀의 mixture를 갱신한다.
- 배경 component에 match되지 않는 픽셀을 foreground로 표시한다.
- foreground pixels를 connected components로 묶는다.
- 위치와 크기를 이용해 track을 이어간다.

발표자 스크립트:
> 전체 흐름은 이렇게 볼 수 있습니다. 프레임이 들어오면 각 픽셀의 mixture model과 비교합니다. 자주 보이고 안정적인 component를 배경으로 골라 현재 픽셀이 거기에 속하는지 판단합니다. 속하지 않으면 foreground mask에 남깁니다. 그 다음 foreground pixels를 connected component로 묶고, 위치와 크기 정보를 이용해서 프레임 간 track으로 연결합니다. 여기서 논문의 핵심 기여는 tracking 알고리즘 자체보다, tracking이 쓸 수 있을 만큼 안정적인 foreground mask를 실시간으로 만드는 배경 모델입니다.

전환 문장:
> 이 구조가 어떻게 행동하는지는 주요 파라미터를 보면 더 명확해집니다.

### Slide 12. 파라미터 직관: 기억 속도와 배경의 폭

발표 시간: 1.8분

핵심 메시지: `K`, `alpha`, `T`, `2.5 sigma`는 각각 기억 용량, 적응 속도, 배경 다양성, local threshold를 조절한다.

화면 구성:
- 4개의 parameter block.
- 각 block은 슬라이더 형태로 tradeoff를 보여준다.

구체 디자인:
- `alpha`: 느린 적응 <-> 빠른 적응.
- `T`: 보수적 배경 <-> 넓은 배경.
- `K`: 적은 모드 <-> 많은 모드.
- `2.5 sigma`: Gaussian별 local acceptance range.
- 지나치게 장식하지 않고, 각 block 안에 한 문장만 넣는다.

본문 텍스트:
- `K`: 한 픽셀이 기억할 수 있는 후보 수.
- `alpha`: 모델이 얼마나 빨리 과거를 잊고 새 관측을 반영하는가.
- `T`: 배경으로 인정할 component의 누적 weight 폭.
- `2.5 sigma`: 전역 threshold가 아니라 component별 local threshold.

발표자 스크립트:
> 이 방법의 행동은 파라미터로 조절됩니다. K는 한 픽셀이 기억할 수 있는 상태 수입니다. alpha는 기억의 속도입니다. 작으면 안정적이지만 변화에 늦고, 크면 빠르게 적응하지만 전경을 배경으로 흡수할 위험이 있습니다. T는 배경의 폭입니다. 낮으면 가장 강한 하나의 배경에 가깝고, 높으면 반복적으로 움직이는 배경 상태까지 받아들입니다. 2.5 sigma 기준은 전역 threshold가 아니라 각 Gaussian의 분산에 따라 달라지는 local threshold입니다.

전환 문장:
> 이제 이 설계가 왜 현실 배경에서 강점을 갖는지 세 가지 상황으로 정리하겠습니다.

### Slide 13. 왜 작동하는가: 세 가지 현실 상황

발표 시간: 2.2분

핵심 메시지: 다중 모드 배경, 느린 조명 변화, 사라진 배경의 복구를 한 구조 안에서 처리한다.

화면 구성:
- 3열 scenario layout.
- 각 열은 상황, 모델 반응, 발표 해석의 3줄 구조.

구체 디자인:
- 상황별 아이콘:
  - 반복 배경: `fa-water`
  - 조명 변화: `fa-sun`
  - 배경 복구: `fa-rotate-left`
- 각 열 하단에 짧은 결론 문장을 청록색으로 강조.

본문 텍스트:
- 반복 배경: 물결, 나뭇잎, 반사는 여러 background component로 남을 수 있다.
- 느린 조명 변화: online update로 평균과 weight가 이동한다.
- 배경 복구: 사라진 원래 배경 component가 mixture 안에 남아 있으면 다시 빠르게 회복된다.

발표자 스크립트:
> 이 모델이 설득력을 갖는 이유는 현실적인 세 상황을 한 구조 안에서 설명하기 때문입니다. 첫째, 물결이나 나뭇잎처럼 배경이지만 계속 바뀌는 경우 여러 component를 배경으로 둘 수 있습니다. 둘째, 햇빛처럼 천천히 변하는 조명은 online update를 통해 평균과 weight가 따라갑니다. 셋째, 물체가 잠시 멈춰서 새 배경처럼 편입되더라도, 원래 배경 component가 완전히 사라지지 않았다면 물체가 사라진 뒤 빠르게 복구될 수 있습니다.

전환 문장:
> 논문은 이 구조를 장기 실시간 운용이라는 형태로 검증합니다.

### Slide 14. 실험 결과: 정확도 경쟁보다 장기 운용 증거

발표 시간: 2.3분

핵심 메시지: 논문의 결과는 현대식 benchmark score보다 장기간 실시간 시스템으로 작동했다는 engineering evidence에 가깝다.

화면 구성:
- 큰 숫자 4개를 dashboard 형태로 배치.
- 우측에는 "해석" 블록.
- 하단에는 실패 사례를 작게 예고.

구체 디자인:
- 숫자는 54px, `#2f7568`.
- 지표:
  - 160x120
  - 11-13 fps
  - 16개월+
  - 차량 33대 / 사람 34명
- 배경은 밝게, 숫자 패널은 흰색과 얇은 border.

본문 텍스트:
- SGI O2, R10000에서 160x120 프레임을 11-13fps로 처리.
- 다섯 개 장면에서 16개월 이상 tracking 정보 저장.
- 10분 장면에서 차량 33대와 사람 34명 추적.
- 빠른 구름 변화 등 급격한 조명 변화는 안정화까지 시간이 필요.

발표자 스크립트:
> 결과를 볼 때 주의할 점은, 이 논문이 오늘날처럼 공개 데이터셋에서 precision, recall을 비교하는 방식의 논문은 아니라는 것입니다. 대신 저자들은 장기간 실제 시스템으로 운용했다는 점을 강하게 제시합니다. 당시 하드웨어인 SGI O2, R10000에서 160x120 영상을 초당 11에서 13프레임 처리했고, 다섯 개 장면에서 16개월 이상 tracking 정보를 저장했습니다. 10분 장면에서는 차량 33대와 사람 34명을 추적했다고 보고합니다. 핵심 성과는 최고 정확도라기보다, 실외 장면에서 장시간 버티는 실시간 배경 모델을 보였다는 점입니다.

전환 문장:
> 물론 이 방식이 모든 문제를 해결한 것은 아닙니다. 한계도 분명합니다.

### Slide 15. 한계: 픽셀 통계만으로는 부족한 것들

발표 시간: 1.8분

핵심 메시지: 이 논문은 강력한 고전이지만, 의미 이해, 그림자 분리, 객체 겹침, 급격한 변화에는 한계가 있다.

화면 구성:
- 좌측: 4개 한계 카드.
- 우측: "무엇의 한계인가?"라는 해석 블록.

구체 디자인:
- 한계 카드는 벽돌색 accent border.
- 아이콘:
  - 픽셀 독립: `fa-border-none`
  - 그림자: `fa-cloud`
  - 겹침: `fa-people-arrows`
  - 급격한 조명: `fa-bolt`
- 우측 해석 블록은 어두운 배경.

본문 텍스트:
- 픽셀 독립 가정: 주변 구조와 물체 형태를 직접 보지 않는다.
- 그림자: 명시적 shadow removal이 아니다.
- 겹침/교차: connected component와 tracking에서 혼동된다.
- 급격한 조명 변화: `alpha`보다 빠른 변화에는 안정화 시간이 필요하다.
- 현대 기준 정량 평가가 부족하다.

발표자 스크립트:
> 한계도 명확합니다. 첫째, 픽셀을 독립적으로 보기 때문에 주변 픽셀의 형태나 물체 구조를 직접 이해하지 못합니다. 둘째, 그림자를 명시적으로 제거하지 않습니다. 감시 목적에서는 어두운 물체를 놓치지 않는 것이 더 중요할 수 있지만, 정확한 객체 마스크가 필요한 응용에서는 한계입니다. 셋째, 두 사람이 붙어 걷거나 차량이 같은 위치에서 교차하면 connected component와 tracking이 혼동됩니다. 넷째, 조명이 갑자기 바뀌면 모델이 따라가는 데 시간이 필요합니다. 결국 이 모델은 의미를 이해하는 모델이 아니라, 픽셀 색 통계로 현실 배경을 견디는 모델입니다.

전환 문장:
> 그래서 이 논문은 최종 해법이라기보다 이후 연구의 기준점으로 보는 것이 정확합니다.

### Slide 16. 현대적 위치: 문제 정의의 기준점

발표 시간: 1.3분

핵심 메시지: 이 논문은 background subtraction을 online background modeling 문제로 정식화했고, 이후 GMM, 샘플 기반, RPCA, 딥러닝 계열의 출발점이 되었다.

화면 구성:
- 상단: 4방향 계보 map.
- 중앙: 최종 평가 문장.
- 하단: Q&A 유도 문장 3개.

구체 디자인:
- 계보는 가로 방향:
  - Improved GMM / MOG2
  - Sample-based models
  - Robust PCA
  - Deep foreground segmentation
- 각 방향은 작은 라벨과 한 줄 설명.
- 중앙 문장은 32px, 청록 강조.

본문 텍스트:
- 남긴 것 1: 배경은 고정 이미지가 아니라 시간적으로 학습되는 모델.
- 남긴 것 2: 같은 픽셀에도 여러 정상 상태가 있을 수 있다.
- 남긴 것 3: foreground/background 판단과 model update가 동시에 일어난다.
- 마무리: 오래된 방법이지만, 고정 카메라 배경 제거 문제를 설명하는 기본 언어를 만들었다.

발표자 스크립트:
> 마무리하면, 이 논문은 현대 딥러닝 segmentation과 비교하면 단순합니다. 하지만 단순하기 때문에 오히려 배경 제거 문제의 핵심 구조를 잘 보여줍니다. 배경은 고정 이미지가 아니라 시간적으로 학습되는 모델이고, 같은 픽셀에도 여러 정상 상태가 있을 수 있으며, 현재 프레임의 판단은 다음 프레임의 배경 기억을 바꿉니다. 이 세 가지가 이 논문이 남긴 중요한 언어입니다. 이후 MOG2, 샘플 기반 배경 모델, Robust PCA, 딥러닝 기반 foreground segmentation은 모두 다른 방식으로 이 문제를 계속 풀어간다고 볼 수 있습니다.

Q&A 유도 문장:
- 왜 `w / sigma`가 배경 score로 적절한가?
- 정지한 전경 물체는 언제 배경이 되는가?
- 딥러닝 시대에도 이 모델을 baseline으로 설명할 가치가 있는가?

## 3. 슬라이드 제작 시 SVG 재작성 지침

### `seminar_problem_timeline.svg`

직접 사용하지 않는다. 다음 정보만 재사용한다.

- 기존 방식의 흐름: 비적응 배경 -> 평균 배경 -> 단일 Gaussian -> mixture model.
- 핵심 문장: 배경은 한 장의 고정 이미지가 아니다.
- 재작성 위치: Slide 3, Slide 4, Slide 6.
- 새 디자인: timeline과 비교 패널을 HTML grid로 재작성. 텍스트가 길면 줄임.

### `seminar_gmm_intuition.svg`

직접 사용하지 않는다. 다음 정보만 재사용한다.

- cluster 3개: 배경 후보 A, 배경 후보 B, 전경 후보.
- 판단 기준: weight, variance, background score.
- 재작성 위치: Slide 7, Slide 10.
- 새 디자인: 반투명 ellipse와 색 점을 CSS 도형으로 직접 구성. 텍스트는 우측 해석 블록으로 분리.

### `seminar_method_pipeline.svg`

직접 사용하지 않는다. 다음 정보만 재사용한다.

- 처리 흐름: 현재 프레임 -> 픽셀별 기억 -> 배경 후보 선택 -> 전경 마스크 -> 추적.
- 핵심 문장: 분류와 학습이 동시에 일어난다.
- 재작성 위치: Slide 9, Slide 11.
- 새 디자인: 6단 파이프라인을 균등 폭으로 재작성. 마지막 tracking 단계도 충분한 폭을 확보.

## 4. 발표 흐름 요약

1. 이 논문은 움직이는 물체를 찾는 논문처럼 보이지만, 실제 핵심은 변하는 배경을 계속 기억하는 방법이다.
2. 단일 배경 이미지나 평균 배경은 현실의 다중 상태 배경을 견디지 못한다.
3. Gaussian mixture는 한 픽셀이 반복적으로 보는 여러 색 덩어리를 동시에 기억한다.
4. 매 프레임에서 match, update, replacement가 일어나며 판단과 학습이 동시에 진행된다.
5. `w / sigma`와 `T`를 통해 자주 보이고 안정적인 component를 배경으로 고른다.
6. 결과의 의미는 현대식 정확도 점수보다 장기 실시간 운용 증거에 있다.
7. 한계는 픽셀 독립성, 의미 부재, 그림자, 겹침, 급격한 변화다.
8. 최종적으로 이 논문은 background subtraction을 online background modeling 문제로 정식화한 기준점이다.

## 5. 이후 실제 HTML 슬라이드 생성 우선순위

실제 HTML/CSS 슬라이드를 만든다면 다음 순서로 제작한다.

1. Slide 1: 제목 슬라이드와 발표자 정보 레이아웃 확정.
2. Slide 2: 전체 디자인 톤과 핵심 관점 표현 확정.
3. Slide 7: GMM intuition을 깨지지 않는 새 도표로 구현.
4. Slide 11: method pipeline을 새 도형으로 구현.
5. Slide 8-10: 수식과 parameter 슬라이드의 가독성 검증.
6. Slide 14-16: 결과, 한계, 계보 슬라이드 완성.

가장 중요한 검증 기준:

- 1280x720에서 텍스트가 넘치지 않는다.
- 긴 한국어 문장이 카드 안에서 깨지지 않는다.
- `<pre><code>` 블록 앞에 불필요한 공백이 렌더링되지 않는다.
- SVG 원본을 직접 사용하지 않아도 같은 메시지가 전달된다.
- 슬라이드만 봐도 발표 흐름이 따라가고, 스크립트는 슬라이드를 읽는 수준을 넘어 해석을 제공한다.

