> 본 포스팅은 [D3.js 공식 문서](https://d3js.org/)를 참고한 포스팅입니다. 오역, 피드백 등은 댓글을 남겨주세요!

- D3.js는 데이터를 기반으로 document를 조작할 수 있게 만드는 자바스크립트 라이브러리입니다. 
- D3.js는 데이터에 HTML, SVG, CSS를 사용하여 활기를 불어넣어줍니다.
- D3.js는 웹 표준을 강조하기 때문에 강력한 시각화 구성요소와 DOM 조작에 대한 데이터 중심 접근 방식을 결합하여 사유 프레임워크에 얽매이지 않고도 최신 브라우저의 모든 기능을 사용할 수 있습니다.

최신 버전(7.0.1)은 이곳에서 다운로드할 수 있습니다.

- [d3-7.0.1.tgz](https://registry.npmjs.org/d3/-/d3-7.0.1.tgz)

최신버전을 직접 link하고 싶다면 아래 코드를 사용할 수 있습니다.

```html
<script src="https://d3js.org/d3.v7.min.js"></script>
```

[모든 소스와 테스트](https://github.com/d3/d3)는 Github에서 사용할 수 있습니다.

- [다운로드](https://github.com/d3/d3/zipball/main)



## Introduction

D3를 사용하면 임의 데이터를 DOM(Document Object Model)에 바인딩한 다음 데이터 중심 변환을 document에 적용할 수 있습니다.
예를 들어 D3을 사용하여 숫자 배열에서 HTML 테이블을 생성할 수 있습니다. 또는 동일한 데이터를 사용하여 부드러운 전환과 인터랙션이 있는 SVG 막대 차트를 만들 수 있습니다.

D3는 상상할 수 있는 모든 특징을 제공하고자 하는 모놀리식 프레임워크가 아닙니다. 
대신 D3는 데이터 기반의 효율적인 문서 조작이라는 문제의 핵심을 해결합니다. 
따라서 독점적 표현을 피하고 뛰어난 유연성을 제공하므로 HTML, SVG 및 CSS와 같은 웹 표준의 모든 기능이 노출됩니다. 
최소한의 오버헤드로 D3는 상호 작용 및 애니메이션을 위한 대규모 데이터셋과 동적 동작을 지원하므로 매우 빠릅니다. 
D3의 기능적 스타일은 다양한 [공식 API](https://github.com/d3/d3/blob/main/API.md) 및 [커뮤니티 개발 모듈](https://www.npmjs.com/browse/keyword/d3-module)을 통해 코드 재사용이 가능합니다.



## Selections

[W3C DOM API](https://www.w3.org/DOM/DOMTR)를 사용하여 문서를 수정하는 것은 지루합니다. 메서드 이름은 너무 상세하며 명령적 접근 방식이기 때문에 임시 상태를 수동으로 반복하고 기록해야 합니다. 

예를 들어, <p>태그의 텍스트 색상을 변경하려면 아래와 같이 코드를 작성해야 합니다.

```js
var paragraphs = document.getElementsByTagName("p");
for (var i = 0; i < paragraphs.length; i++) {
  var paragraph = paragraphs.item(i);
  paragraph.style.setProperty("color", "blue", null);
}
```

D3은 선언적 접근 방식을 채택하여 `selection`이라고 하는 임의 노드 집합에서 작동합니다.
예를 들어, 위의 루프를 다음과 같이 다시 작성할 수 있습니다.

```js
d3.selectAll("p").style("color", "blue");
```

그러나 필요에 따라 개별 노드를 조작할 수도 있습니다.

```js
d3.select("body").style("background-color", "black");
```



`Selectors`는 W3C Selectors API에 의해 정의되며 최신 브라우저에서 기본적으로 지원됩니다. 

위의 예제는 태그 이름(`<p>` 및 `<body>`)별로 노드를 선택합니다. 

Element는 container, 속성 값, 클래스 및 ID 등 다양한 술어를 사용하여 선택할 수 있습니다.



D3은 속성 또는 스타일 설정, 이벤트 리스너 등록, 노드 추가, 제거 또는 정렬, HTML 또는 텍스트 콘텐츠 변경 등 노드를 변경하는 다양한 방법을 제공합니다. 

이것들은 대부분의 욕구를 충족시키기에 충분합니다. 각 D3의 `Selection`은 단순히 노드 배열이기 때문에 기본 DOM에 직접 액세스할 수도 있습니다.



## Dynamic Properties

[jQuery](https://jquery.com/)와 같은 다른 DOM 프레임워크에 익숙한 독자는 D3와의 비슷함을 알아차렸을 겁니다. 

그러나 스타일, 속성 및 기타 속성은 단순한 상수가 아니라 D3의 `데이터 함수`로 지정할 수 있습니다. [`d3.geoPath` ](https://github.com/d3/d3-geo/blob/main/README.md#geoPath) 함수와 같이 이러한 기능은 겉보기에는 단순하지만 놀라울 정도로 강력합니다. 

예를 들어, [지리 좌표](https://tools.ietf.org/html/rfc7946)를 SVG [경로 데이터](https://www.w3.org/TR/SVG/paths.html#PathData)에 넣게 된다면, D3는 area, line 및 pie 차트에 대한 [그래픽 원형](https://github.com/d3/d3-shape)을 비롯한 다양한 재사용 가능 기능과 기능 팩토리를 기본으로 제공합니다.

예를 들어, 문단에 무작위로 색상을 지정하려면 아래와 코드를 작성할 수 있고,

```js
d3.selectAll("p").style("color", function() {
  return "hsl(" + Math.random() * 360 + ",100%,50%)";
});
```

회색 그림자가 번갈아 나타나기 위해서는,

```js
d3.selectAll("p").style("color", function(d, i) {
  return i % 2 ? "#fff" : "#eee";
});
```

계산된 속성은 바인딩된 데이터를 참조하는 경우가 많습니다. 

데이터는 값의 배열로 지정되고 각 값은 선택 함수에 첫 번째 인수(d)로 전달됩니다. 

기본 `join-by-index`기능을 사용하면 데이터 배열의 첫 번째 요소가 선택 영역의 첫 번째 노드에 전달되고 두 번째 요소가 두 번째 노드에 전달되는 등의 작업을 수행할 수 있습니다. 

예를 들어, 숫자 배열을 문단 요소에 바인딩하는 경우 다음 숫자를 사용하여 동적 글꼴 크기를 계산할 수 있습니다.

```js
d3.selectAll("p")
  .data([4, 8, 15, 16, 23, 42])
    .style("font-size", function(d) { return d + "px"; });
```

데이터가 문서에 바인딩된 후에는 데이터 연산자를 생략할 수 있습니다. D3은 이전에 바인딩된 데이터를 검색합니다. 이렇게 하면 재바인딩 없이 속성을 다시 계산할 수 있습니다.



## Enter and Exit

D3의 `Enter` 및 `Exit` selection을 사용하여 수신 데이터에 대한 새 노드를 생성하고 더 이상 필요하지 않은 송신 노드를 제거할 수 있습니다.

데이터가 selection에 바인딩되면 데이터 배열의 각 요소가 선택 항목의 해당 노드와 쌍을 이룹니다. 

데이터보다 노드가 적은 경우 추가 데이터 요소가 `Enter Selection`을 형성하며, 입력 선택 항목에 추가하여 인스턴스화할 수 있습니다. 

```js
d3.select("body")
  .selectAll("p")
  .data([4, 8, 15, 16, 23, 42])
  .enter().append("p")
    .text(function(d) { return "I’m number " + d + "!"; });
```

노드 업데이트는 데이터 연산자의 결과인 디폴트 `selection`입니다. 따라서 `enter` 및 `exit` 을 잊은 경우 해당 데이터가 있는 요소만 자동으로 선택합니다. 

일반적인 패턴은 초기 선택을 수정할 `updating node`, 추가할 `entering node` , 제거할 `exiting node`의 세 부분으로 나누는 것입니다.

```js
// Update…
var p = d3.select("body")
  .selectAll("p")
  .data([4, 8, 15, 16, 23, 42])
    .text(function(d) { return d; });

// Enter…
p.enter().append("p")
    .text(function(d) { return d; });

// Exit…
p.exit().remove();
```

이 세 가지 경우를 별도로 처리하면 어떤 노드에서 어떤 작업을 실행할지 정확하게 지정할 수 있습니다. 따라서 성능이 향상되고 전환에 대한 제어력이 향상됩니다. 

예를 들어 막대 차트를 사용할 때, old scale로 entering 막대를 생성한 다음 new scale로 updating 및 exiting 막대와 함께 entering 막대를 새로 전환할 수 있습니다.

D3을 사용하면 데이터를 기반으로 문서를 변환할 수 있습니다. 여기에는 요소 생성 및 파괴가 모두 포함됩니다. D3을 사용하면 사용자 상호 작용, 시간에 따른 애니메이션 또는 서드파티 앱의 비동기식 알림에 대해서도 기존 문서를 변경할 수 있습니다. 

문서가 서버에서 처음 렌더링되고 D3을 통해 클라이언트에서 업데이트되는 하이브리드 접근 방식도 가능합니다.



## Transformation, not Representation

D3는 새로운 시각적 표현을 도입하지 않습니다. [Processing](https://processing.org/)이나 [Protovis](https://mbostock.github.io/protovis/)와 달리 D3의 그래픽 마크 어휘는 HTML, SVG, CSS 등의 웹 표준에서 직접 가져옵니다. 

예를 들어, D3을 사용하여 SVG 요소를 작성하고 외부 스타일시트로 스타일을 지정할 수 있습니다. 복합 필터 효과, 점선 및 클리핑을 사용할 수 있습니다. 

구글에서 내일 크롬에 새로운 기능을 도입하면 툴킷 업데이트 없이 즉시 사용할 수 있습니다. 또한 향후 D3 이외의 툴킷을 사용하기로 결정한 경우 표준에 대한 지식을 가져갈 수 있습니다.

무엇보다도 D3은 브라우저의 내장 요소 검사기를 사용하여 쉽게 디버깅할 수 있습니다. D3으로 조작하는 노드는 브라우저가 기본적으로 이해하는 노드입니다.



## Transitions

D3는 `animated transitions`를 자연스럽게 확장시키는데 초점을 맞춥니다. 변환은 시간이 지남에 따라 스타일과 속성을 점진적으로 보간합니다. `Tweening`은`elastic`, `cubic-in-out`, `linear`과 같은 쉬운 기능을 통해 제어할 수 있습니다. 

D3의 interpolator는 문자열에 포함된 숫자와 숫자(글꼴 크기, 경로 데이터 등) 및 복합 값과 같은 원형을 모두 지원합니다. D3의 interpolator 레지스트리를 확장하여 복잡한 속성 및 데이터 구조를 지원할 수도 있습니다.

예를 들어, 페이지 배경을 검은색으로 희미하게 하려면:

```js
d3.select("body").transition()
    .style("background-color", "black");
```

또는 symbol map의 원 크기를 시차적 지연으로 조정하려면:

```js
d3.selectAll("circle").transition()
    .duration(750)
    .delay(function(d, i) { return i * 10; })
    .attr("r", function(d) { return Math.sqrt(d * scale); });
```

이렇게 할 수 있습니다.

D3는 실제로 변경되는 특성만 수정함으로써 오버헤드를 줄이고 높은 프레임률에서 그래픽 복잡성을 높일 수 있습니다. D3는 또한 이벤트를 통한 복잡한 전환의 시퀀싱도 허용합니다. CSS3 전환도 사용할 수 있습니다.

 D3은 브라우저의 도구 상자를 대체하지 않고 사용하기 쉬운 방식으로 노출합니다.



> 더 배우고 싶다면 이 [튜토리얼](https://observablehq.com/@d3/learn-d3)을 읽어보세요
