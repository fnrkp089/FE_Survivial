# ❤ Design System

## 반응형 웹 디자인

반응형 웹 디자인은 다양한 디바이스 크기에 대응하는 접근 방식이다.\
즉  태블릿, 휴대폰, 텔레비젼 등 어떤 디바이스에서도 화면에 맞게 \
크기와 레이아웃을 조정하여 최적의 사용자 경험을 제공한다

보통 유동 그리드, 유동 이미지, 미디어 쿼리를 사용하여 반응형 컨텐츠들을 생성한다.

반응형 웹 디자인은 별도의 기술이 아니다라는 것을 이해하는 것이 중요하다.\
즉, 웹 디자인에 대한 접근 방식이나 콘텐츠를 보는데 사용되는 장치에 반응할 수 있는 레이아웃 생성에 사용되는 모범 사례 집합을 기술하는 데 사용되는 용어다.\


### 미디어 쿼리

미디어 쿼리를 사용하면 사용자의 화면이 특정 너비나 해상도를\
넘어가는지  판단 후,  CSS를 선택적으로 적용하여 \
사용자의 요구에 맞게 스타일을 지정할 수 있다.

미디어 쿼리는 **화면(screen), 티비(tv), 프린터(print)와 같은 미디어 타입(media type)**과 \
적어도 하나 이상의 표현식(expression)으로 구성된다.\
표현식은 **width, height, color**와 같은 미디어 특성(media feature)들을 이용하여 그 특성들의 상태에 따라 다른 스타일 시트를 적용할 수 있습니다. 미디어 쿼리는 CSS3에 포함되어 있으며, 컨텐츠의 변경없이 주로 화면의 크기에 따라 스타일 시트를 달리하여 적절한 모양을 보여줄 수 있다.\


모바일을 우선할 경우 다음과 같은 순서로 작성이 된다.

```css
/* 모바일에 적용될 스타일을 먼저 작성한다. */

@media screen and (min-width: 769px) {
	/* 데스크탑에서 사용될 스타일을 여기에 작성합니다. */
}
```

데스크탑을 우선할 경우에는 다음과 같은 순서로 작성한다.

```css
/* 데스크탑에서 사용될 스타일을 먼저 작성한다. */

@media screen and (max-width: 768px) {
	/* 모바일에 사용될 스트일 시트를 여기에 작성합니다. */
}
```

그 이유는 중단점에 있다.\
중단점이란. 미디어쿼리에서 레이아웃이 변경되는 지점을 뜻한다. \
중단점을 사용할 때는 절대 단위가 아닌 상대 단위로 정의하는것이 좋다.\
그렇기 때문에 일반적으로 화면이 좁은 모바일과 같은 디바이스의 레이아웃을 토대로 \
더넓은 화면의 레이아웃을 구현하는 편이다.\


### 다중 열(Multicol)

다중 열을 사용하면 열의 개수나 너비만큼 콘텐츠를 분할할 수 있다.

```css
.container {
  column-count: 3;
}

.container {
  /* 폰트 크기의 10배 */
  column-width: 10em;
}
```

### FlexBox

[flexbox Froggy](https://flexboxfroggy.com/#ko)

[flexbox defense](http://www.flexboxdefense.com/)

### grid

&#x20;Grid는 2차원으로 수평 수직을 동시에 영역을 나눌 수 있다.

<figure><img src="../.gitbook/assets/image (3).png" alt=""><figcaption></figcaption></figure>

마치 신문처럼 각 부분을 공간으로 나눈다.



### flex

1차원 레이아웃 시스템이라고 생각하면된다.\
수직, 수평중 하나를 택하는것이고, 한방향으로만 나아간다.

## 디자인 시스템

> [Laura Kalbag의 “Design Systems” 소개](https://24ways.org/2012/design-systems/)

> [Laura Kalbag의 “Design Systems” 슬라이드](https://speakerdeck.com/laurakalbag/design-systems-1)

> [Nielsen Norman Group의 “Design Systems 101”](https://www.nngroup.com/articles/design-systems-101/)

👉 Summary: A design system is a set of **standards** to manage design **at scale** by **reducing redundancy** while creating a **shared language** and **visual consistency** across different pages and channels.\
