# Web Core Vital의 세 가지 지표

## 1. 계기

- 뽀송뽀송아이님의 5주차 발표, 모달 UX 분석에서 살짝 언급된 Web Core Vital
- 타 스터디에서 들음
- 구글,
    2020년 5월, 우수한 사용자 경험이란 무엇인가에 대한 발표(코어 웹 바이탈)
    2021년 5월, 구글의 검색 결과 페이지에 사용자 경험을 표시되게 하겠다
 
    -> 사용자 경험이 그 자체로 중요할 뿐만 아니라, 검색 순위에도 영향을 미칠 수 있을 것
       따라서 앞으로 이 지표에 대해 이해하는게 앞으로의 프론트엔드 개발시 중요해질 수도 있음

## 2. 개요 

### LCP (Largest Contentful Paint)
### FID (First Input Delay)
### CLS (Cumulative Layout Shift)

- 각각의 의미
- 측정 기준과 측정 툴
- 이 지표가 나빠지는 주요 원인

## 3. LCP (Largest Contentful Paint)

콘텐츠 중에서 메인 콘텐츠가 표시되기까지 얼마나 걸리는가?
-> 사용자가 맥락을 이해할 수 있는 콘텐츠가 표시되는데 얼마나 걸리나가 사용자 경험에 관련있다는 논리
   웹 사이트 내에서 일단 뭐든지 표시하는 것만으로는 부족

### 측정 기준과 측정 툴
구글이 제공하는 Lighthouse, Chrome DevTools 등에서 측정

    2.5초 이하이면 좋고,
    2.5초에서 4초 사이는 개선이 필요,
    4초 이상이면 문제가 있음

### 이 지표가 나빠지는 주요 원인

#### 서버에서의 응답이 느림
    - 서버를 최적화
    - 유저가 가까운 CDN을 사용하도록
    - 캐쉬를 사용


#### 자바스크립트나 CSS에 의해서 렌더링이 중단
    - JS, CSS를 최적화
    - 덜 중요한 JS, CSS는 Defer 옵션
    - 인라인을 검토

#### 리소스 로드가 느림
    <img>, <image>, <svg>, <video> 등이 해당

    - 굳이 거기서 보여줘야하는지 검토
    - 이미지를 압축
    - 새로나온 이미지 포맷으로 바꾼다 (JPEG 2000, JPEG XR, or WebP)
    - 반응형 이미지를 쓴다
    - 중요한 리소스는 Preload한다
    
## 4. FID (First Input Delay)
    콘텐츠가 표시되고 사용자가 읽게 된 시점부터, 조작이 가능해질때까지의 입력을 지연시키는 시간.
 
### 측정 기준과 측정 툴

- 사용자의 체감. 시뮬레이션을 통해 측정 할 수 없음
- 다만, Lighthouse, Chrome DevTools에서 제공하는 TBT(Total Blocking Time)라는 지표로 어느 정도 예측할 수 있고, 이 지표를 개선하는 과정에서 FID도 개선되기를 기대할 수 있음

0.1초 이하면 좋고, 0.1에서 0.3초 사이면 개선이 필요
0.3초 이상이면 문제가 있음

### 이 지표가 나빠지는 주요 원인

#### 무거운 자바스크립트

 - defer/async 옵션을 통해 자바스크립트를 읽는 타이밍을 개선
 - 자바스크립트를 분할(code split)
 - 폴리필을 안하는걸 검토 (모던 브라우저용으로 JS를 번들)
 - 사용되지 않는 JS는 지운다
 - 무거운 처리는 Web Worker를 사용하는걸 검토한다

### CLS (Cumulative Layout Shift)
 뉴스 기사를 보려고 들어간 웹사이트에서 기사 링크를 클릭하려는 순간 레이아웃이 이동해서 광고가 나타나 기사가 아닌 광고를 클릭한 경험.

 어떤 페이지에 들어갔을 때 갑작스럽게 발생하는 레이아웃 이동의 정도를 합산 이동 거리라는 개념을 도입해서 만들어낸 지표

### 측정 기준과 측정 툴
구글이 제공하는 Lighthouse, Chrome DevTools 등에서 측정

0.1 이하의 CLS라면 양호한 것이고, 0.1~ 0.25라면 개선이 필요한 것이고 0.25 이상이면 나쁜 상태

### 이 지표가 나빠지는 주요 원인

- width나 height를 지정하지 않을 경우
- 웹 폰트를 스왑되거나 렌더링될 때 레이아웃 사이즈가 갑자기 변경되는 경우가 있음 (FOUT, FOIT)
    
## 참고

- https://www.ascentkorea.com/core-web-vitals/
- https://web.dev/optimize-lcp/
- https://web.dev/optimize-fid/
- https://web.dev/optimize-cls/
- Front-End Study #2「Performance Tuning in depth」 15분~
  https://www.youtube.com/watch?v=Ga8P_buwXnw
