> 본 글은 Fabian Sebastian 님의 [Modality Is the One UX Concept That Most Designers Don’t Fully Understand](https://uxplanet.org/modality-the-one-ux-concept-you-need-to-understand-when-designing-intuitive-user-interfaces-e5e941c7acb1) 를 참고한 포스팅입니다. 오역, 피드백 등은 답글을 달아주세요!


### 본론에 앞서...
많은 디자이너들이 그들의 **느낌**에 따라서 디자인을 하곤 한다.
물론 이 **느낌**이 많은 상황에서 멀쩡히 작동하고 있지만, 당신의 **느낌**을 대신해서 상당히 잘 짜여진 UI를 구성할 수 있도록 도와주는 검증된 기준들이 있다.

본 포스팅에서는 "Modality"의 기준들에 대해서 탐색하고 왜 오직 두 종류의 스크린이 존재하는 지, 그리고 앱과 웹사이트가 Information architecture와 user flow를 직관적인 UI로 변환하는데 실패한 이유들에 대해서 이야기해 보려고 한다. 

우선 다음 주장으로 시작해보자.
### 스크린은 오직 두 종류만 존재한다.
**1. Modal 스크린
2. Non-Modal 스크린**

모든 viewport는 이 두 종류 중 하나로 결정된다. 이 둘의 차이를 알아보기 전에 Modal 스크린이 무엇인지에 대해 정의해보자.

### Modal 스크린이란 무엇일까
![](https://images.velog.io/images/dnr6054/post/5ced914a-21ca-40d0-9707-a103f0a63c3c/image.png)

Modal 스크린은 여러 모양과 크기가 있다.
- Fullscreen Modal Views
- Popups
- Pop-Overs
- Lightboxes
- Alerts/Notifications
- Dialogs
- ...

Modal 스크린과 Non-Modal 스크린 둘 다 child view, 즉 Main window의 하위 항목이지만, 한가지 큰 차이점이 있다.

> "A modal window creates a mode that disables the main window, but keeps it visible with the modal window as a child window in front of it. Users must interact with the modal window before they can return to the parent application" - Wikipedia

대부분의 Modal 스크린(특히 Desktop application에서)은 쉽게 식별할 수 있다. 왜냐하면 간단히 Main Window를 덮어쓰기 때문이다. 

그러나 모바일 기기에서의 스크린 크기는 **제한적**이다. 이것이 모바일 기기에서의 많은 Modal 스크린들이 모든 화면을 잡아먹는 이유이다. 이들은 더이상 Main Window를 밑에서 보여주지 않으며 Non-Modal 스크린과 식별하기 어렵게 만든다.
![](https://images.velog.io/images/dnr6054/post/d765ca46-253b-4cff-9fea-e0542495005e/image.png)

가장 큰 차이점은 우리가 각각의 스크린과 **어떻게 상호작용하느냐**에 존재한다. Non-Modal 스크린이 우리를 단지 부모 스크린으로 갈 수 있게 한다면, Modal 스크린은 메인 스크린으로 가기 이전에 유저로 하여금 어떤 동작을 수행하거나 취소하도록 요구한다.

Non-Modal 스크린의 가장 뚜렷한 시각적 구별은 **네비게이션의 표시여부**이다. Non-Modal 스크린은 유저로 하여금 이전 네비게이션 단계에서도 앞뒤로 점프할 수 있게 한다. 그 스크린이 더 하위 단계에 있음에도 말이다.
반면에 Modal 스크린은 이전 네비게이션 단계를 사용하기 위해 `저장`이나 `취소`와 같은 작업을 통해 창을 닫아야 한다.

### 왜 Modality를 사용해야 할까?
Modal 스크린은 간단한 문제를 해결한다. 유저는 쉽게 주의를 잃기 떄문에 그들의 집중을 잡아야 한다. Modal 스크린이 정확히 그 역할을 한다. 사람들이 넘어가기 전에 **각각의 단일 작업에 집중**할 수 있게 한다.
> "Modality creates focus by preventing people from doing other things until they complete a task or dismiss a message or view"
	- Apple

### 언제 Modality를 사용해야 할까.
이제 우리는 Modal 스크린이 어떻게 생겼는지 알고, Non-Modal 스크린과 어떻게 구분해야 하는지 알며, 그 목적 또한 안다. 이제 어떤 상황에 써야할지 알아보자.

한번 데이터베이스에 유저들이 귀여운 고양이 GIF를 올리고 보며 댓글을 달 수 있는 앱을 만든다고 가정해보자. 
![](https://images.velog.io/images/dnr6054/post/f5f8ccf2-7560-42f1-9759-9719dab281bb/c246823715e09da1260ef1c8498837119821aa2c.gif)

간단한 유저플로우는 아마 다음과 같을 것이다.
1. 유저가 앱을 연다.    `메인 스크린`
2. 여러 활성화된 탭들 중 하나에 들어간다.     `고양이 목록 스크린`
3. 고양이들 중 하나를 클릭한다.    `고양이 상세보기 스크린`
4. 그리고 댓글 달기를 누른다.    `댓글 달기 스크린`

![](https://miro.medium.com/max/2000/1*TesjjLJz9LJ0ln7qozVUwQ.jpeg)

그리고 유저는 각 단계에서 추가 동작을 할 수 있다. 예를 들어 고양이 목록 스크린에서 다른 고양이를 추가할 수도 있으며, 고양이 상세보기 스크린에서 데이터를 수정할 수도 있다. 

이제 어떤 스크린이 Modal이고 어떤게 아닐까? 우린 다음과 같은 규칙을 사용해볼 수 있다.

> "Use Modal Screens for self-contained processes, use Non-Modal Screens for everything else."	- Fabian Sebastian, the original author

여기서 `self-contained process`는 명확한 시작지점과 종료지점을 갖는 모든 프로세스를 말한다. 이프로세스를 수행하는 제한된 시간 동안 이는 유저를 일반적인 유저플로우에서 끄집어 낸 다음 다시 시작한 곳으로 되돌려 놓는다. 

구글은 이를 다음과 같이 표현했다.
> "Use Modal Screens(dialogs) for Critical information that requires a specific user task, decision, or acknowledgement"	- Google

이를 우리의 고양이 앱에서 보면, 유저 플로우에서 본 네가지 스크린은 Modal이 아니다. 그러나 고양이를 추가한다던지, 수정하거나 댓글을 다는 것 같은 행동은 모달이 되는 것이다.

![](https://miro.medium.com/max/2000/1*qzNQJW28h_c8VgDEaBwifQ.jpeg)

모든 Modal의 동작들은 유저가 다시 메인 플로우로 돌아가기 전에 **취소**되거나 **성공적으로 완료**되어야 한다. 이런 이유로 Modal 스크린은 이전 버튼 대신 `취소`나 `저장` 버튼을 사용한다. 만약 당신의 이전 버튼이 저장하는 액션을 촉발한다면 그 화면을 `취소`와 `저장`버튼이 있는 Modal 스크린으로 바꾸는 것을 고려해봐야 한다.

그 반대도 마찬가지다. 만약 `취소`와 `저장`버튼이 Modal 스크린에서 같은 역할을 해서 별 의미가 없다면 이를 Non-Modal로 바꿀 수 있다. 이 경우 네비게이션도 화면에 계속 표시되어야 한다.

이제 다시 고양이 앱으로 돌아가 보자. 아마 우리의 앱은 다음과 같은 인터페이스를 가질 것이다.

![](https://miro.medium.com/max/2000/1*dE-FHjoPDGKlt04IzF-lpw.jpeg)

실제 세계에서 Modal 과 Non-Modal 스크린의 경계는 사실 좀 모호하다. 예를 들어 대부분의 앱에서 이미지의 전체화면 보기는 대부분 모달이다. 그게 딱히 어떤 프로세스도 아니면서 말이다. Modal 스크린은 우리의 관심을 끌기 위한 특정한 상황에서도 쓰일 수 있다. 만약 우리의 고양이 상세보기 스크린이 수정이나 댓글이 없는 end-point view라면 우린 modality를 썼을 수도 있다. 그러나 그 화면에서 우리가 설계한 앱은 유저가 Information architecture의 더 깊은 곳으로 가거나 다양한 추가 작업을 할 수 있기 때문에 명확한 endpoint가 없고, 그렇기 때문에 메인 플로우, 즉 Non-Modal 스크린이라는 것이다. 

어떤 작업이 `self-contained` 인지 판단하고, 그리고 Modal을 사용할지 말지 결정하는 것은 결국 디자이너의 책임이다. 만약 모호한 경우에는 애플의 말을 기억하자.

> "Minimize the use of modality. Generally, people prefer to interact with apps in nonlinear ways. Consider creating a modal context only when it’s critical to get someone’s attention, when a task must be completed or abandoned to continue using the app, or to save important data." - Apple

`FYI:` 물론 인터페이스는 Modal과 Non-Modal을 엄격하게 구분하지 않고도 완벽하게 작동할 수 있다. 그러나 Modality는 Apple, Google, Microsoft 및 여러 기업의 인터페이스 생태계에 깊이 내재되어 있으며 유저는 이에 대해 상응하는 기대치가 형성되어 있다. 

### 어떻게 Modality가 사용되어야 할까?
이제 우리는 Modality를 언제 사용해야 하는 지에 대해 제대로 이해하고 있다. 이제 남은 궁금점은
"어떻게 디자인해야해?" 일것이다. 여기에 Modal 스크린을 위한 간단한 참고사항들이 있다.

- 항상 `닫기` 버튼을 보여준다. 유저가 앱 안에서 길을 잃으면 쉽게 끄고 top level로 이동할 수 있다. 
- 안드로이드와 iOS에서 닫기 버튼은 대부분 상단 왼쪽에 위치한다. 안드로이드는 `X` 아이콘을 선호하고 iOS는 `취소` 텍스트를 선호하지만 아이콘 버튼도 iOS에서 매우 흔하고 별로 거부감이 없다.
- `저장` 버튼은 iOS와 안드로이드 둘 다 기본적으로 상단 오른쪽에 있다. 그러나 이 위치는 큰 기기에서는 좀 클릭하기 어렵다. 그러므로 스크린 아래에 고정적으로 저장버튼을 띄우거나 인라인으로 최하단에 저장버튼을 띄워주는 대안이 있다.
![](https://miro.medium.com/max/2000/1*nF_B6N_k9A0okgXIakrIcQ.jpeg)

#### Multi Step Modals
Modial 스크린이 여러 스텝이나 하위 스크린을 포함하면 좀 더 복잡해진다. 기본적으로 Continue 버튼은 상단 오른쪽에 있으며, 그 다음 스크린은 새로운 Modal을 띄우지 않고 그 Modal 안에서 Non-Modal 스크린처럼 표시한다. 

만약 위에서 추천한 것 처럼 저장, 적용, 계속과 같은 버튼을 스크린 하단에 띄운다면 모달의 상단 오른쪽은 공간이 비게 되어 취소 버튼을 추가할 수 있다. 이렇게 되면 왼쪽에서 오른쪽으로 취소 버튼이 점프하게 되지만, 이런 기능을 제공하지 않는 것 보다는 훨씬 낫다.

![](https://miro.medium.com/max/2000/1*Ukl4JFAG9U5rvhrIc4jeeA.jpeg)

#### 애니메이션
지금까지는 iOS와 안드로이드가 모달 뷰를 사용하는 방식에서 상당히 유사하다. 그러나 이는 애니메이션을 보면 생각이 바뀔 것이다.

- iOS: 애니메이션은 iOS에서 상당히 표준화 되어있다. Non-Modal 스크린은 오른쪽에서 프레임 안으로 밀어 들어오며 탭 바는 여전히 스크린 하단에 위치한다. 또한 이 애니메이션은 `edge-swipe` 제스처를 취할 때 뒤로가기를 수행하는 것과 맞아 떨어진다. 
반면에 Modal 스크린은 프레임 하단에서 안으로 미끄러져 들어가 인터페이스를 오버레이 하며 `edge-swipe` 제스처를 허용하지 않는다. 만약 저장할 것이 없다면 위에서 아래로 끌어내리는 제스처를 쓸 수 있다.

- 안드로이드: 안드로이드의 애니메이션은 훨씬 더 다양하다. Google은 `Material Design Guide`에서 의미있는 전환을 사용할 것을 권장한다. 상단 네비게이션 바가 희미해지는 동안 자식 element는 터치 시 살짝 들어올려져서 확장된다. 
**그러나** 안드로이드에서는 Modal과 Non-Modal 스크린 애니메이션을 구분하지 않는다.

### 결론
많은 디자이너들이 그들의 **느낌**에 따라서 제작하곤 한다. 그리고 이 **느낌**이 때로는 표준보다 중요하기도 하다. 그러나 표준을 알고 그걸 적용할지 말지 결정하는 것은 중요하다.

Modality는 앱에서 가장 무시되고 있는 UX 원리 중 하나라고 생각한다. 크로스 플랫폼 앱과 하이브리드 앱에서는 플랫폼 지침과 표준에 정확히 맞도록 만들어지지 않는다. **그러나 Modality의 일반적인 개념은 필요할 때 그것을 깨기 위해서 알아야만 하는 가이드라인이다.**
