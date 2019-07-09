# 💻📖 hacker-laws

**개발자에게 유용한 법칙, 이론, 원칙, 그리고 패턴들**

<br>

<!-- vim-markdown-toc GFM -->

* [서론](#서론)
* [법칙](#법칙)
    * [암달의 법칙](#암달의-법칙)
    * [브룩스의 법칙](#브룩스의-법칙)
    * [콘웨이의 법칙](#콘웨이의-법칙)
    * [던바의 숫자](#던바의-숫자)
    * [갈의 법칙](#갈의-법칙)
    * [핸런의 면도날](#핸런의-면도날)
    * [호프스태터의 법칙](#호프스태터의-법칙)
    * [허트버의 법칙](#허트버의-법칙)
    * [하이프 사이클 & 아마라의 법칙](#하이프-사이클—아마라의-법칙)
    * [하이럼의 법칙 (암시적 인터페이스의 법칙)](#하이럼의-법칙-암시적-인터페이스의-법칙)
    * [무어의 법칙](#무어의-법칙)
    * [파킨슨의 법칙](#파킨슨의-법칙)
    * [성급한 최적화의 법칙](#성급한-최적화의-법칙)
    * [푸트의 법칙](#푸트의-법칙)
    * [복잡성 보존의 법칙 (테슬러의 법칙)](#복잡성-보존의-법칙-테슬러의-법칙)
    * [허술한 추상화의 법칙](#허술한-추상화의-법칙)
    * [사소함의 법칙](#사소함의-법칙)
    * [유닉스 철학](#유닉스-철학)
    * [스포티파이 모델](#스포티파이-모델)
    * [와들러의 법칙](#와들러의-법칙)
* [원칙](#원칙)
    * [파레토의 원리 (80 : 20의 법칙)](#파레토의-원리-80--20의-법칙)
    * [견고함의 원칙 (포스텔의 법칙)](#견고함의-원칙-포스텔의-법칙)
    * [솔리드](#솔리드)
    * [단일 책임 원칙](#단일-책임-원칙)
    * [개방-폐쇄 원칙](#개방-폐쇄-원칙)
    * [리스코프 치환 원칙](#리스코프-치환-원칙)
    * [인터페이스 분리 원칙](#인터페이스-분리-원칙)
    * [의존 관계 역전 원칙](#의존-관계-역전-원칙)
    * [DRY 원칙](#dry-원칙)
    * [YAGNI](#yagni)
* [추천 도서](#추천-도서)
* [TODO](#todo)

<!-- vim-markdown-toc -->

<br>

## 서론

개발을 이야기할 때 흔히 논하는 법칙들이 있습니다. 이 저장소는 그 중 가장 보편적인 것들에 대한 참조와 개요입니다. 공유와 PR 제출 부탁드려요!

❗: 이 저장소는 여러 법칙, 원칙, 그리고 패턴에 관한 설명을 포함하고 있지만, 그 중 어떤 것도  _지지_ 하고 있지 않습니다. 그것들을 적용하여야 할지에 말지에 대해서는 언제나 논의의 여지가 있으며, 또한 당신이 어떤 작업을 하느냐에 따라서도 크게 달라집니다.

<br>

_(이 글은 https://github.com/dwmkerr/hacker-laws 의 번역입니다.)_

<br>

## 법칙

### 암달의 법칙

[위키피디아의 암달의 법칙](https://ko.wikipedia.org/wiki/암달의_법칙)

> 암달의 법칙은 시스템에 리소스를 추가함으로써 얻을 수 있는 컴퓨터 작업 성능 향상의 최대 폭을 나타내주는 공식이다. 일반적으로 병렬 컴퓨팅에서 이를 이용하여, 프로세서 개수의 증가가 프로그램 자체의 구조적인 병렬화 제한에 맞서 실제적으로 가져다주는 이득을 예측할 수 있다.

예시를 살펴보자. 어떠한 프로그램이 단일 프로세서로 구동되어야 하는 부분 A와 병렬화될 수 있는 부분 B로 이루어져있다고 할 때, 우리는 프로세서의 추가적인 투입이 제한된 이득만을 가져다줌을 알 수 있다. B 부분의 성능을 크게 향상시킬 수 있지만, A 부분의 속도는 그대로 남을 것이기 때문이다.

아래의 그래프는 성능 향상 가능성의 예시를 보여준다.

![Diagram: Amdahl's Law](./images/amdahls_law.png)

*(이미지 출처: Daniels220 @영어 Wikipedia, Creative Commons Attribution-Share Alike 3.0 Unported, https://en.wikipedia.org/wiki/File:AmdahlsLaw.svg)*

<br>

보다시피 50%나 병렬화 가능한 프로그램임에도 10개 프로세서 이후에는 거의 이득이 없는 반면, 95% 병렬화 가능한 프로그램은 수천 개가 추가될 때까지도 유의미한 성능 향상을 보여주고 있다.

[무어의 법칙](#무어의-법칙)과 개별 프로세서의 성능 증가 속도가 완화되면서, 병렬화는 최적화의 핵심이 되었다. 그래픽스 프로그래밍이 이에 대한 가장 알맞은 예시이다. 셰이더 기반의 최신 컴퓨팅에서는 개별 픽셀 혹은 프래그먼트를 병렬로 렌더링할 수 있는데, 이것이 최신 그래픽 카드들이 대개 수천 개의 코어(GPU 또는 셰이더 유닛)로 구성된 이유이다.

<br>

참고:

- [브룩스의 법칙](#브룩스의-법칙)
- [무어의 법칙](#무어의-법칙)

<br>

### 브룩스의 법칙

[위키피디아의 브룩스의 법칙](https://ko.wikipedia.org/wiki/브룩스의_법칙)

> 지체되는 소프트웨어 개발 프로젝트에 인력을 더하는 것은 개발을 늦출 뿐이다.

이 법칙은 이미 늦어지고 있는 소프트웨어 개발을 빨리하기 위해 사람을 더 투입하는 것은 도리어 완성을 늦출 뿐이라고 말한다. 브룩스는 이것은 비록 극도로 단순화한 이야기임을 분명히 했으나, 다만 일반적으로 보았을 때 자원 투입 시간과 의사소통 비용으로 인해 단기적으로 속도가 줄어들 수 있다고 하였다. 또한 많은 작업들은 분할할 수 없기 때문에, 즉 인력이 늘어난다고 하여 쉽게 분배할 수 없기 때문에, 기대할 수 있는 속도 증가 역시 낮다.

흔히 말하는 "임산부 9명이 모여도 아기를 한 달만에 낳을 수는 없다"는 구절은 브룩스의 법칙 중에서도, 특정 작업은 나누거나 병렬화할 수 없음을 비유적으로 뜻한다.

이것은 그의 저서 '[맨먼스 미신](#추천-도서)'의 주요한 주제이다.

<br>

참고:

- [Death March](#todo)
- [추천 도서 : 맨먼스 미신](#추천-도서)

<br>

### 콘웨이의 법칙

[Conway's Law on Wikipedia](https://en.wikipedia.org/wiki/Conway%27s_law)

이 법칙에 따르면 시스템의 구조는 설계하는 조직의 구조를 반영한다. 이것은 조직 개선을 시도할 때 종종 인용되고는 하는데, 가령 조직이 여러 개의 작고 끊어진 단위로 구성되어 있다면 거기에서 나온 소프트웨어 또한 그 모습을 닮는다고 한다. 또한 만약 조직이 기능과 서비스를 중심으로 수직적으로 짜여 있다면, 이 역시 소프트웨어가 이러한 모습을 반영할 것이란 것이다.

<br>참고:

- [스포티파이 모델](#스포티파이-모델)

<br>

### 던바의 숫자

[위키피디아의 던바의 숫자](https://ko.wikipedia.org/wiki/던바의_숫자)

"Dunbar's number is a suggested cognitive limit to the number of people with whom one can maintain stable social relationships— relationships in which an individual knows who each person is and how each person relates to every other person." There is some disagreement to the exact number. "... [Dunbar] proposed that humans can comfortably maintain only 150 stable relationships." He put the number into a more social context, "the number of people you would not feel embarrassed about joining uninvited for a drink if you happened to bump into them in a bar." Estimates for the number generally lay between 100 and 250.

Like stable relationships between individuals, a developer's relationship with a codebase takes effort to maintain. When faced with large complicated projects, or ownership of many projects we lean on convention, policy, and modeled procedure to scale. Dunbar's number is not only important to keep in mind as an office grows, but also when setting the scope for team efforts or deciding when a system should invest in tooling to assist in modeling and automating logistical overhead. Putting the number into an engineering context, it is the number of projects (or normalized complexity of a single project) for which you would feel confident in joining an on-call rotation to support.

<br>

참고:

- [Conway's Law](#conways-law)

<br>

### 갈의 법칙

[Gall's Law on Wikipedia](https://en.m.wikipedia.org/wiki/John_Gall_(author)#Gall's_law)

> 잘 작동하는 복잡한 체계는 항상 잘 작동하던 간단한 체계에서 발전한다. 처음부터 복잡하게 설계된 체계는 절대로 작동하지 않으며 잘 돌아가도록 만들 수도 없다. 언제나 작동하는 간단한 시스템에서 출발해야 한다.
>
> ([존 갈](https://en.m.wikipedia.org/wiki/John_Gall_(author)))

갈의 법칙은 고도로 복잡한 시스템을 _설계_하려는 시도는 대개 실패함을 암시한다. 고도로 복잡한 체계는 하루아침에 이루어진 것이 아니라, 더 간단한 체계로부터 진화한 것이다.

고전적인 예시는 월드 와이드 웹이다. 현재의 웹의 상태는 굉장히 복잡하다. 그러나 처음에는 그저 학술 기관 간의 간편한 컨텐트 공유 시스템으로서 시작했을 뿐이다. 이러한 목적을 성공적으로 달성하였기 때문에 시간이 지남에 따라 복잡한 시스템으로 진화할 수 있었다.

<br>

참고:

- [KISS (Keep It Simple, Stupid)](#TODO)

<br>

### 핸런의 면도날

[위키피디아의 핸런의 면도날](https://ko.wikipedia.org/wiki/핸런의_면도날)

> 어리석음으로 충분히 설명이 되는 일을 악의의 탓으로 돌리지 말라.
>
> — 로버트 J. 핸런

이 법칙에 따르면 부정적인 결과를 낳는 행동은 악의로부터 비롯된 것이라기보다는, 행동과 그것이 불러올 파장에 대한 몰이해 때문이다.

<br>

### 호프스태터의 법칙

[Hofstadter's Law on Wikipedia](https://en.wikipedia.org/wiki/Hofstadter%27s_law)

> 설령 호프스태터의 법칙을 고려하더라도, 일은 마치는 건 언제나 예상보다 오래 걸린다.
>
> — 더글라스 호프스태터

무언가가 얼마나 걸릴지 짐작할 때 이 법칙을 인용하는 것을 들을 수 있을지 모른다. 뻔한 말 같지만, 우리는 소프트웨어를 개발함에 있어 결과를 내놓기까지의 기간을 예상하는 것에 그다지 능하지 않다.

이는 '[괴델, 에셔, 바흐: 영원한 황금 노끈](#추천-도서)'에서 나온 말이다.

<br>

참고:

- [추천 도서 : 괴델, 에셔, 바흐: 영원한 황금 노끈](#추천-도서)

<br>

### 허트버의 법칙

[Hutber's Law on Wikipedia](https://en.wikipedia.org/wiki/Hutber%27s_law)

> 개선은 악화를 의미한다.
>
> ([패트릭 허트버](https://en.wikipedia.org/wiki/Patrick_Hutber))

이 법칙의 주장에 따르면 시스템의 개선은 다른 부분의 악화로 이어지거나 다른 악화를 숨겨, 현 상태로부터 전체적인 질적 저하를 불러오게 된다.

예를 들어 특정 엔드 포인트의 응답 시간 감소로 인해 요청 흐름에 있어서 스루풋과 용량 이슈가 늘어날 수 있고, 이는 전혀 다른 부분에 영향을 끼칠 수 있다.

<br>

### 하이프 사이클 & 아마라의 법칙

[위키피디아의 하이프 사이클](https://ko.wikipedia.org/wiki/하이프_사이클)

> 우리는 새로운 기술의 효과를 단기적으로는 과대평가하고, 장기적으로는 과소평가하는 경향이 있다.
>
> — 로이 아마라

하이프 사이클은 미국의 정보 기술 연구 및 자문 회사인 가트너에서 시간의 흐름에 따른 기술에 대한 기대와 성숙도를 시각적으로 나타낸 것이다.

<br>

![The Hype Cycle](./images/gartner_hype_cycle.png)

*(이미치 출처: Jeremykemp @영어 Wikipedia, CC BY-SA 3.0, https://commons.wikimedia.org/w/index.php?curid=10547051)*

<br>

즉, 이 사이클에 따르면 대개 신기술과 그 전망에 대하여 거품이 촉발된다. 이때 많은 팀들은 너무 빠르게 뛰어들었다가 결과물에 종종 실망하고는 한다. 이것은 어쩌면 기술이 아직 덜 성숙하기 때문이거나, 혹은 실제 세계에의 적용이 덜 이루어졌기 때문일 것이다.

특정 시점이 지나고 나면 기술 자체의 역량과 실제적인 적용의 기회가 늘어나고, 마침내 생산성을 얻을 수 있게 된다. 로이 아마라는 이를 가장 간결한 문장으로 정리하였다. "우리는 새로운 기술의 효과를 단기적으로는 과대평가하고, 장기적으로는 과소평가하는 경향이 있다".

<br>

### 하이럼의 법칙 (암시적 인터페이스의 법칙)

[Hyrum's Law Online](http://www.hyrumslaw.com/)

> API에 충분한 수의 유저가 있다면,
>
> 명세에서 지정된 것은 아무런 상관이 없다:
>
> 시스템에서 관측될 수 있는 모든 행동 양식은
>
> 다른 이들에게 달려있을 것이다.
>
> — 하이럼 라이트

하이럼의 법칙에 따르면 API에 충분히 많은 수의 소비자가 있을 때, API의 모든 행동 양식은 궁극적으로 명세에 있는 정의가 아닌 아닌 다른 누군가에게 달려있게 된다. 간단한 예시를 들자면 가령 API의 응답 시간과도 같은 비함수적 요소들이다. 좀 더 구체적인 예시는 에러 메세지에 정규 표현식을 이용하여 API의 에러의 *타입* 을 알아내는 소비자들을 들 수 있다. API의 공개 명세에서는 메세지의 내용에 관하여서 아무 것도 알려주지 않으며 대신 에러 코드를 사용해야 한다고 하고 있더라도, 어떤 유저들은 메세지를 사용하거나 메세지의 내용을 변경하여 API를 사실상 붕괴시킬 수 있다.

<br>

참고:

- [허술한 추상화의 법칙](#허술한-추상화의-법칙)
- [XKCD 1172](https://xkcd.com/1172/)

<br>

### 무어의 법칙

[위키피디아의 무어의 법칙](https://ko.wikipedia.org/wiki/무어의_법칙)

> 집적 회로의 트랜지스터 수는 대략 2년마다 2배가 된다.

반도체와 기판 기술의 가파른 성장 속도를 설명하기 위한 무어의 예측은 1970년대부터 2000년대 후반까지 굉장히 정확한 것으로 드러났다. 최근에는 [부품 소형화의 물리적 한계](https://ko.wikipedia.org/wiki/터널_효과)로 인하여 약간 둔화되긴 하였지만 말이다. 하지만 병렬화와 반도체 기술의 혁신적 변화에 대한 가능성, 그리고 양자 컴퓨팅은 무어의 법칙이 향후 몇 십 년간에도 들어맞을 수 있음을 의미할 수도 있다.

<br>

### 파킨슨의 법칙

[Parkinson's Law on Wikipedia](https://en.wikipedia.org/wiki/Parkinson%27s_law)

> 작업은 남은 기한을 채울 때까지 늘어난다.

원래 맥락에서 이 법칙은 관료제에 대한 연구를 기반으로 하고 있다. 소프트웨어 개발 계획에서도 비관적으로 적용될 수 있는데, 개발자들은 기한이 다가오기 전에는 효율적이지 못하다가 기한이 가까워지면 급하게 일을 하게 되므로 결국 실제적인 데드라인을 흐릿하게 한다.

만일 이 법칙이 [호프스태터의 법칙](#호프스태터의-법칙)과 결합된다면, 더욱 비관적인 관점에 도달할 수 있다. 작업은 남은 시간을 채우기 위해 늘어나면서도 *예정된 시간보다 길어지기까지 할 것이다.*

<br>참고:

- [호프스태터의 법칙](#호프스태터의-법칙)

<br>

### 성급한 최적화의 법칙

[Premature Optimization on WikiWikiWeb](http://wiki.c2.com/?PrematureOptimization)

> 성급한 최적화는 모든 악의 근원이다.
>
> [(도널드 커누스)](https://ko.wikipedia.org/wiki/도널드_커누스)

도널드 커누스의 논문 [Goto문을 이용한 구조적 프로그래밍](http://wiki.c2.com/?StructuredProgrammingWithGoToStatements)에 따르면, "프로그래머들은 프로그램에서 중요하지 않은 부분을 최적화하는 것을 생각하고 또 걱정함으로써 어마어마한 시간을 낭비하는데, 이런 시도는 디버깅이나 유지보수를 고려하면 오히려 효율성에 막대하게 부정적인 영향을 끼친다. 우리는 가령 97% 정도의 경우에, 작은 부분의 효율성에 관하여 생각하지 않아야 한다 : **성급한 최적화는 모든 악의 근원이다.** 그러나 나머지 결정적인 3%의 경우에까지 기회를 저버리면 안 된다."

_성급한 최적화_ 란 (좁은 의미로) 그것이 꼭 필요한지 알기 전에 행해지는 최적화라고 할 수 있다.

<br>

### 푸트의 법칙

[Putt's Law on Wikipedia](https://en.wikipedia.org/wiki/Putt%27s_Law_and_the_Successful_Technocrat)

> 기술은, 자신이 관리하지 않는 것들을 이해하는 자들과, 자신이 관리하는 것들을 이해하지 못하는 자들 두 가지 분류의 사람들에 의해 지배된다.

푸트의 법칙에는 종종 다음 푸트의 귀결이 따라붙는다:

> 모든 기술 조직의 계급에서는 시간이 흐르면서 역량의 역전이 일어난다.

이 문구에 따르면 조직 구성론에 대한 여러 가지 선택 기준과 유행 변화에 따라서, 조직에는 여러 명의 숙련된 노동 계층과 자신들이 관리하는 일의 복잡도와 어려움을 모르는 여러 명의 관리직이  생기게 된다. 이것은 [피터의 원리](#TODO) 혹은 [딜버트의 법칙](#TODO)과도 같은 현상 때문이다.

다만 이런 류의 법칙에서 잊지 말아야 할 점은 이러한 모호한 일반화는 _일부_ 조직에는 적용될 수도 있으나, 나머지에는 아니라는 점이다.

<br>

참고:

- [피터의 원리](#TODO)
- [딜버트의 법칙](#TODO)

<br>

### 복잡성 보존의 법칙 (테슬러의 법칙)

[The Law of Conservation of Complexity on Wikipedia](https://en.wikipedia.org/wiki/Law_of_conservation_of_complexity)

이 법칙에 따르면 시스템에는 더 이상 줄일 수 없는 특정한 정도의 복잡성이 존재한다.

시스템에 있어 어떤 종류의 복잡성은 '의도되지 않은 것'이다. 그것은 빈약한 구조, 실수, 혹은 문제에 대한 그릇된 모델링의 대가이다. 이러한 의도되지 않은 복잡성은 줄이거나 없앨 수 있다. 반면에, 풀어야 할 문제에 대하여 '내재적'으로 자리하는 복잡성이 있다. 이러한 복잡성은 옮겨질 수는 있으나 없앨 수는 없다.

이 법칙이 시사하는 흥미로는 점은, 설령 전체 시스템을 단순화하더라도 내재적인 복잡성은 줄어드는 것이 아니라 _사용자에게 전이되어서_, 이용을 더욱 복잡하게 만든다.

<br>

### 허술한 추상화의 법칙

[The Law of Leaky Abstractions on Joel on Software](https://www.joelonsoftware.com/2002/11/11/the-law-of-leaky-abstractions/)

> 모든 사소하지 않은 추상화는, 어느 정도, 허술하다.
>
> —조엘 스폴스키

이 법칙에 따르면 컴퓨팅에서 복잡한 시스템과 작업하기 위해 일반적으로 사용되는 추상화에서는 때에 따라 하단 요소의 '누수'가 일어날 수 있고, 이는 추상화가 예상치 못한 방향으로 전개되게 한다.

파일을 불러와 내용을 읽는 상황을 살펴보자. 파일 시스템 API는 로우 레벨 커널 시스템의 _추상화_ 인데, 이 시스템 또한 자기 플래터(혹은 플래시 메모리나 SSD)의 데이터를 물리적으로 변경하는 것의 추상화이다. 대부분의 경우 파일을 이진 데이터의 스트림으로서 추상화하는 것은 문제가 없을 것이다. 그러나 자기 디스크에서는 데이터를 순서대로 읽는 것이 임의 접근보다 *비교할 수 없을 만큼* 빠른 반면에(페이지 폴트 비용 때문에), SSD에서는 전혀 상관이 없다. 내부 구현을 상세히 이해하여야 이런 경우에 대처할 수 있는데(가령, 데이터베이스 인덱스 파일은 임의 접근의 비용을 줄이도록 구조가 짜여져 있다), 이렇듯 추상화는 개발자가 모르면 곤란하도록 내부 구현 상세를 '누출'한다.

위의 예시는 _더 많은_ 추상화가 도입되면 더욱 복잡해질 수 있다. 리눅스 운영체제는 네트워크를 경유하여 파일에 접근할 수 있도록 하면서도 로컬에서는 '일반' 파일로 취급한다. 이런 추상화는 네트워크 오류가 발생하면 '허술해질' 것이다. 만약 개발자가 이런 파일들을 네트워크 지연이나 오류에 대한 고려 없이 '일반' 파일로 취급한다면, 버그가 생길 것이다.

이 법칙을 설명하는 글에 따르면 하부 구동 원리를 모른 채로 추상화에 과도하게 의존할 경우, 도리어 문제 해결을 복잡하게 만들 수 있다고 하고 있다.

<br>

참고:

- [하이럼의 법칙](#하이럼의-법칙-암시적-인터페이스의-법칙)

<br>실제 사례:

- [포토샵의 느린 초기 로딩](https://forums.adobe.com/thread/376152) - 과거에 마주한 문제이다. 포토샵은 종종 켜는 데에 몇 분씩이나 걸리기도 하는데, 이 문제는 구동 시작시에 현재 기본으로 설정된 프린터의 정보를 읽어오는 것에서 발생하였다. 만약 그 프린터가 네트워크 프린터라면 극도로 오랜 시간이 걸리게 되는 것이다. 시스템에 네트워크 프린터의 _추상화_ 가 로컬 프린터와 유사하게 제공된 점은 연결 상태가 좋지 못한 상황의 사용자에게 문제를 일으켰다.

<br>

### 사소함의 법칙

[The Law of Triviality on Wikipedia](https://en.wikipedia.org/wiki/Law_of_triviality)

이 법칙은 정작 심각한 혹은 중요한 것들보다 사소한 이슈들 혹은 외양에 훨씬 더 많은 시간을 쏟게 됨을 시사한다.

가상의 예시로서, 위원회가 원자력 발전소에 건설 계획을 허가하는 과정에서 훨씬 중요한 발전소 자체의 설계는 놔두고 자전거 보관소 얘기나 하는 데에 시간을 쏟는 것을 들 수 있다. 거대하고 복잡한 주제의 논의에서 그 분야의 전문 지식이나 사전 준비 없이 뭔가 유용한 이야기를 할 수는 없을 것이다. 그러나 사람들은 자신이 기여하는 것처럼 보여지고 싶어하고, 따라서 쉽게 해결될 수 있으며 그다지 중요한 것은 아닌 작은 디테일에 너무 많은 시간을 쏟는 경향이 생겨난다.

이 가상의 일화는 사소한 디테일에 시간 버리는 것을 '자전거보관소한다'고 표현하도록 만들었다.

<br>

### 유닉스 철학

[위키피디아의 유닉스 철학](https://ko.wikipedia.org/wiki/유닉스_철학)

유닉스 철학은 소프트웨어의 구성 요소는 작아야 하며, 하나의 특정한 작업을 잘하도록 해야 한다는 것이다. 작고 단순하며 잘 정의된 단위들을 조합함으로써, 거대하고 복잡하며 다목적인 프로그램을 이용하는 것보다 쉽게 시스템을 설계할 수 있다.

서비스가 작고, 하나의 특정한 작업을 맡으며, 복잡한 행동은 단순한 블록의 조합으로 구성할 수 있는 '마이크로서비스 아키텍쳐' 같은 근래의 관행 또한 이 법칙의 적용으로 생각할 수 있다.

<br>

### 스포티파이 모델

[The Spotify Model on Spotify Labs](https://labs.spotify.com/2014/03/27/spotify-engineering-culture-part-1/)

스포티파이 모델은 '스포티파이'에 의해 유명해진 팀과 조직 구조에 대한 접근법이다. 이 모델에서 팀은 기술보단 기능을 중심으로 구성된다.

스포티파이 모델은 부족, 길드, 지부와 같은 그들 조직 구조의 요소 또한 유명하게 만들었다.

<br>

![Spotify Tribe Engineering Model](./images/spotify_model.jpg)

*(이미지 출처: https://medium.com/@media_75624/exploring-key-elements-of-spotifys-agile-scaling-model-471d2a23d7ea)*

<br>

### 와들러의 법칙

[Wadler's Law on wiki.haskell.org](https://wiki.haskell.org/Wadler's_Law)

> 프로그래밍 언어를 설계할 때, 이 기능 목록에 나온 항목들을 논의하는 데 걸리는 총 시간은 2의 항목의 번호 제곱에 비례한다.
> 
> 0. 의미론
> 1. 구문론
> 2. 어휘
> 3. 주석다는 법
> 
> (즉, 의미론에 1시간을 쓸 때마다 주석다는 법에 1 곱하기 2의 세제곱인 8시간을 쓴다는 뜻이다.)

[사소함의 법칙](#사소함의-법칙)처럼, 와들러의 법칙에 따르면 언어 구조를 설계할 때 쓰이는 시간은 각 기능의 중요도에 반비례한다.

<br>

참고:

- [사소함의 법칙](#사소함의-법칙)

<br>

## 원칙

원칙들은 일반적으로 설계의 가이드라인과도 같다.

<br>

### 파레토의 원리 (80 : 20의 법칙)

[위키피디아의 파레토 법칙](https://ko.wikipedia.org/wiki/파레토_법칙)

> 세상 대부분의 것들은 균등하게 분배되지 않았다.

파레토의 원리에 의하면, 경우에 따라 대부분의 결과는 소수로부터 비롯된다:

- 어떤 소프트웨어의 80%는 총 시간 중 20%만에 쓰일 수 있다(반대로, 가장 어려운 20%를 만드는 것에 80%의 시간이 든다).
- 20%의 노력이 80%의 결과를 만들어낸다.
- 20%의 일이 80%의 수입을 창출한다.
- 20%의 버그가 80%의 크래쉬를 일으킨다.
- 20%의 기능이 사용량 중 80%를 차지한다.

1940년대에 품질 관리의 아버지로 널리 알려진 미국계 루마니아인 공학자 조셉 주란 박사는, [품질 문제에 파레토의 원리를 적용하기 시작했다](https://en.wikipedia.org/wiki/Joseph_M._Juran).

이 원리는 또한 80 : 20의 법칙, 중요한 소수의 법칙, 혹은 희소 인자의 원리라고도 불리운다.

<br>

실제 사례:

- 2002년 당시 마이크로소프트는 20%의 가장 많이 보고된 버그를 고침으로써, 윈도우즈와 오피스에서 80%의 관련 에러와 크래쉬가 사라졌다고 하였다([출처](https://www.crn.com/news/security/18821726/microsofts-ceo-80-20-rule-applies-to-bugs-not-just-features.htm)).

<br>

### 견고함의 원칙 (포스텔의 법칙)

[위키피디아의 견고함의 원칙](https://ko.wikipedia.org/wiki/견고함의_원칙)

> 당신이 하는 일은 엄하게, 남의 것을 받아들일 때는 너그럽게.

종종 서버 어플리케이션 개발에 있어, 이 원칙에 따르면 보내는 것은 최대한 간략하면서도 명세를 철저히 따르도록 하되, 받는 것은 설령 명세를 따르지 않더라도 처리할 수 있는 한 받아들이는 것을 지향해야 한다고 한다.

이 원칙의 목적은 의미가 분명한 입력의 경우 비록 형식적으로는 빈약하더라도 이해는 할 수 있으므로 이를 수용함으로써 견고한 시스템을 설계하는 것이다. 다만 그러한 기형의 입력을 받아들임에 있어 특히 입력을 제대로 테스트하지 않을 경우, 보안 위협의 가능성이 생길 수 있다.

<br>

### 솔리드

이는 다음에 대한 약자이다:

* S: [The Single Responsibility Principle (단일 책임 원칙)](#단일-책임-원칙)
* O: [The Open/Closed Principle (개방-폐쇄 원칙)](#개방-폐쇄-원칙)
* L: [The Liskov Substitution Principle (리스코프 치환 원칙)](#리스코프-치환-원칙)
* I: [The Interface Segregation Principle (인터페이스 분리 원칙)](#인터페이스-분리-원칙)
* D: [The Dependency Inversion Principle (의존 관계 역전 원칙)](#의존-관계-역전-원칙)

이것은 [객체지향 프로그래밍](#todo)의 핵심 원칙이다. 이러한 설계 원칙들은 개발자들이 유지보수 가능한 시스템을 짓는 것을 도울 수 있다.

<br>

### 단일 책임 원칙

[위키피디아의 단일 책임 원칙](https://ko.wikipedia.org/wiki/단일_책임_원칙)

> 모든 모듈과 클래스는 단일한 책임만을 지녀야 한다.

'[솔리드](#솔리드)' 원칙의 첫 번째이다. 이 원칙에 따르면 모듈이나 클래스는 반드시 오직 하나의 일만을 해야 한다. 좀 더 실용적으로 말하자면, 프로그램 기능에 있어서 하나의 작은 변화는 오로지 한 구성 요소만을 바꿔야 함을 뜻한다. 가령, 패스워드 복잡도 검증을 어떻게 처리할지 변경하는 것은 오직 프로그램의 한 곳만을 바꿔야 한다.

이론적으로 이것은 코드를 더욱 견고하게 만들고 수정을 용이하게 한다. 바뀔 구성 요소가 단일 책임만을 지고 있다는 것을 안다면 그 변화에 대한 _테스팅_ 또한 더욱 쉽기 때문이다. 앞서 말한 예시에서, 패스워드 복잡도 관련 구성 요소를 변경하는 것은 오직 패스워드 복잡도 관련 기능에만 영향을 끼친다. 여러 책임을 지고 있는 구성 요소를 바꿀 때에 어떠한 일이 일어날지 예측하는 것은 훨씬 더 어렵다.

<br>

참고:

- [객체지향 프로그래밍](#todo)
- [솔리드](#솔리드)

<br>

### 개방-폐쇄 원칙

[위키피디아의 개방-폐쇄 원칙](https://ko.wikipedia.org/wiki/개방-폐쇄_원칙)

> 개체는 확장에 대해서는 열려 있어야 하고, 수정에 대해서는 닫혀 있어야 한다.

'[솔리드](#솔리드)' 원칙의 두 번째이다. 이 원칙에 따르면 개체(클래스, 모듈, 함수 등)는 행동을 _확장_ 할 수 있어야 하지만, _기존의_ 행동은 고칠 수 없어야 한다.

가상의 예시로서 마크다운 문서를 HTML로 변환할 수 있는 모듈을 상상해보자. 모듈이 내부적인 변경 없이도 새로이 제안된 마크다운 기능을 다룰 수 있도록 확장 가능하다면, 확장에 대해 열려 있는 것이다. 만약 모듈이 소비자에 의해서 기존의 마크다운 기능 처리를 변경할 수 있도록 수정될 수 _없다면_, 수정에 대해 닫혀 있는 것이다.

이 원칙은 특히 [객체지향 프로그래밍](#todo)과 관련이 있는데, 우리는 객체를 쉽게 확장하고 싶은 반면 예상치 못한 방향으로 수정되는 것은 피하고 싶기 때문이다.

<br>

참고:

- [객체지향 프로그래밍](#todo)
- [솔리드](#솔리드)

<br>

### 리스코프 치환 원칙

[리스코프 치환 원칙 ](https://ko.wikipedia.org/wiki/리스코프_치환_원칙)

> 시스템을 파괴하지 않으면서도 자료형을 하위 자료형으로 대체할 수 있어야 한다.

'[솔리드](#솔리드)' 원칙의 세 번째이다. 이 원칙은 만일 어떠한 구성 요소가 자료형에 의존한다면, 시스템 실패나 하위 자료형이 무엇인지에 대한 정보 없이도 하위형을 대신 사용할 수 있어야 한다고 말한다.

가령, 파일을 나타내는 구조로부터 XML 문서를 읽어들이는 메소드가 있다고 하자. 만약 메소드가 '파일' 기반형을 사용하고 있다면, '파일'에서 파생된 모든 것은 해당 함수에서 쓰일 수 있다. '파일'이 역방향 탐색을 지원하고 XML 파서가 그 기능을 이용한다고 할 때 만약 하위 자료형인 '네트워크 파일'에 대한 역방향 탐색 시도 시 실패한다면, '네트워크 파일'은 규율을 위반하고 있는 것이다.

이 원칙은 특히 [객체지향 프로그래밍](#todo)과 관련이 있는데, 자료형의 계층 관계를 세심히 모델링해야  시스템 사용자들의 혼란을 막을 수 있기 때문이다.

<br>

참고:

- [객체지향 프로그래밍](#todo)
- [솔리드](#solid)

<br>

### 인터페이스 분리 원칙

[위키피디아의 인터페이스 분리 원칙](https://ko.wikipedia.org/wiki/인터페이스_분리_원칙)

> 어떠한 클라이언트도 자신이 사용하지 않는 메소드에 의존하도록 강요당하면 안 된다.

'[솔리드](#솔리드)' 원칙의 네 번째이다. 이 원칙에 따르면 구성 요소의 소비자는 구성 요소가 가진 함수들 중에서 실제로 사용하지 않는 것들에 의존하면 안 된다.

예를 들면, 파일을 나타내는 구조로부터 XML 문서를 읽어들이는 메소드가 있다고 하자. 그 메소드는 오직 파일에서의 바이트 읽기, 전진, 그리고 후진 기능만이 필요하다. 만약 이 메소드가 파일 구조의 연관 없는 기능(파일 보안을 위한 권한 업데이트와도 같은)이 변하였다고 해서 업데이트가 필요하다면, 이 원칙은 무효가 된 것이다. 파일이 '탐색 가능 스트림' 인터페이스를 구현하고, XML 리더기가 사용하도록 하는 편이 나을 것이다.

이 원칙은 특히 [객체지향 프로그래밍](#todo)에서 적용되어, 인터페이스, 계층 구조, 그리고 추상 자료형을 통해 구성 요소 간의 [결합도의 최소화](#todo)를 이루려고 한다. [덕 타이핑](#todo)은 명시적 인터페이스를 제거함으로써 이 원칙을 강제한다.

<br>

참고:

- [객체지향 프로그래밍](#todo)
- [솔리드](#solid)

- [덕 타이핑](#todo)
- [디커플링](#todo)

<br>

### 의존 관계 역전 원칙

[위키피디아의 의존 관계 역전 원칙](https://ko.wikipedia.org/wiki/의존관계_역전_원칙)

> 고수준 모듈은 저수준 구현에 의존해서는 안 된다.

'[솔리드](#솔리드)' 원칙의 다섯 번째이다. 고수준에서 지휘하는 구성 요소는 의존 관계를 알 필요가 없다는 원칙이다.

예시로서, 웹사이트의 메타데이터를 읽는 프로그램이 있다고 하자. 우리는 중심 구성 요소가 웹페이지 내용을 다운로드하는 구성 요소와 메타데이터를 읽을 수 있는 구성 요소를 알아야만 한다고 생각할 수 있다. 만약 의존 관계 역전 원칙을 고려한다면, 중심 구성 요소는 오로지 바이트 데이터를 가져올 수 있는 추상 구성 요소와 바이트 스트림에서 메타데이터를 읽을 수 있는 추상 구성 요소에만 의존하면 된다. TCP/IP, HTTP, HTML 등에 대해서는 알 필요가 없다.

이 원칙은 마치 예상되는 의존 관계를 '역전'하는 것처럼 보일 수 있기 때문에 복잡하다(그래서 이러한 이름이 붙었다). 실제로는, 개별 지휘체가 올바른 구현의 추상 자료형이 사용되었는지도 확실시 해야 함을 뜻한다(위의 예시에서 _무언가_ 가 여전히 메타데이터를 읽는 추상 구성 요소에 HTTP 파일 다운로더와 HTML 메타 태그 리더기를 제공해야 한다). 이것은 [제어 반전](#todo)이나 [의존성 주입](#todo)과 같은 패턴으로 이어진다.

<br>

관련:

- [객체지향 프로그래밍](#todo)
- [솔리드](#solid)

- [제어 반전](#todo)
- [의존성 주입](#todo)

<br>

### GLIDE (???)

이는 다음에 대한 약자이다?:

- G: [Gaebang-Pyesoe Wonchik (개방-폐쇄 원칙)](#개방-폐쇄-원칙)
- L: [Liskov Chihwan Wonchik (리스코프 치환 원칙)](#리스코프-치환-원칙)
- I: [Interface Bunli Wonchik (인터페이스 분리 원칙)](#인터페이스-분리-원칙)
- D: [Danil Chakim Wonchik (단일 책임 원칙)](#단일-책임-원칙)
- E: [Euijon Gwangye Yukjun Wonchik (의존 관계 역전 원칙)](#의존-관계-역전-원칙)

이것은 [객체지향 프로그래밍](#todo)의 핵심 원칙이다? 이러한 설계 원칙들은 개발자들이 유지보수 가능한 시스템을 짓는 것을 도울 수 있다?

<br>

### DRY 원칙

[The DRY Principle on Wikipedia](https://en.wikipedia.org/wiki/Don%27t_repeat_yourself)

> 모든 지식은 시스템 내에서 반드시 단일하고, 모호하지 않으며, 권위적인 표현으로 나타나야 한다.

DRY는 _Don't Repeat Yourself반복하지 마라_ 의 약자이다. 이 원칙은 개발자들에게 있어 코드의 반복을 줄이고 정보를 한 곳에 모을 수 있도록 돕기 위해 고안되었으며, 1999년 앤드류 헌트와 데이브 토마스의 저서 [실용주의 프로그래머](https://en.wikipedia.org/wiki/The_Pragmatic_Programmer)에 나와 있다.

> DRY의 반대는 _WET_ (Write Everything Twice모든 것을 두 번 써라, 혹은 We Enjoy Typing저희는 타자치는 게 좋아요)이라 할 수 있겠다.

만일 같은 정보가 둘 혹은 그 이상 곳에 흩어져 있다면, DRY 원칙을 적용하여 하나로 합친 후 원하는/필요한 곳에서 재사용할 수 있다.

<br>

관련:

- [실용주의 프로그래머](https://en.wikipedia.org/wiki/The_Pragmatic_Programmer)

<br>

### YAGNI

[위키피디아의 YAGNI](https://ko.wikipedia.org/wiki/YAGNI)

이것은 _**Y**ou **A**ren't **G**onna **N**eed **I**t넌 필요 없을 거다_ 의 약어이다.

> 언제나 실제로 필요할 때만 구현하고, 절대 혹시 나중에 쓸지도 모르니 만들지 말아라.
>
> ([론 제프리즈](https://twitter.com/RonJeffries)) (XP의 공동 설립자이자 "Extreme Programming Installed : XP 도입을 위한 실전 입문"의 저자)

이 _익스트림 프로그래밍_ (XP) 원칙은 개발자들이 오직 당장 요구될 때에만 기능을 개발하고, 미래를 예측하여 혹시 추후에 필요할지 모르는 기능을 구현하려는 시도를 피하라고 말한다.

이 원칙을 고수한다면 코드베이스에서 사용되지 않는 코드의 양을 줄일 수 있을 것이고, 의미 없는 기능 구현에 시간과 노력을 쏟지 않아도 될 것이다.

<br>

관련:

- [추천 도서 : Extreme Programming Installed : XP 도입을 위한 실전 입문](#추천-도서)

<br>

## 추천 도서

이 개념들이 흥미롭다면, 다음 책들도 즐길 수 있을 것입니다.

- [Extreme Programming Installed : XP 도입을 위한 실전 입문 - 론 제프리즈, 앤 앤더슨, 체트 핸드릭슨](https://www.goodreads.com/en/book/show/67834) - 익스트림 프로그래밍의 핵심 원리를 다룬다.

- [맨먼스 미신 - 프레드릭 P. 브룩스 Jr.](https://www.goodreads.com/book/show/13629.The_Mythical_Man_Month) - 소프트웨어 공학의 고전. [브룩스의 법칙](#브룩스의-법칙)은 이 책의 주요한 주제이다.
- [괴델, 에셔, 바흐 : 영원한 황금 노끈 - 더글라스 R. 호프스태터](https://www.goodreads.com/book/show/24113.G_del_Escher_Bach) - 이 책은 분류하기 어렵다. [호프스태터의 법칙](#호프스태터의-법칙)은 이 책으로부터 비롯되었다.

<br>

## TODO

Hi! If you land here, you've clicked on a link to a topic I've not written up yet, sorry about this - this is work in progress!

Feel free to [Raise an Issue](https://github.com/dwmkerr/hacker-laws/issues) requesting more details, or [Open a Pull Request](https://github.com/dwmkerr/hacker-laws/pulls) to submit your proposed definition of the topic.