# CSS 선택자 실습

이 프로젝트는 CSS 선택자와 기본 스타일을 연습하기 위한 예제입니다.  
HTML 문서와 내부 스타일시트를 사용하여 다양한 선택자와 스타일을 적용합니다.

## 1. 선택자 종류

- **태그 선택자**: 요소 이름 그대로 (예: `p`, `h1`)
- **클래스 선택자**: `.className` (재사용 가능)
- **아이디 선택자**: `#idName` (문서 내 고유)
- **속성 선택자**: 특정 속성 기준 (예: `input[type="password"]`)
- **그룹 선택자**: 여러 선택자 동시 적용 (`h3, .lead`)
- **결합자**: 부모-자식(`>`), 조상-후손(` `), 형제(`+`, `~`) 관계

## 2. CSS 적용 방법

1. **인라인**: `<h1 style="color:red"> ... </h1>`
2. **내부 스타일**: `<style> ... </style>` (head 안 작성)
3. **외부 스타일**: `link` 태그로 별도 .css 파일 연결

## 3. 주요 스타일 예시

- `#brand`: 파란색, 두껍게, 제목 강조
- `.alert`: 빨간색, 경고 문구
- `.lead`: 초록색, 강조 단락
- `input[type="password"]`: 연한 회색 배경
- `a[target="_blank"]`: 보라색 밑줄
- `.section .note`: 회색 글자, 배경 강조 시 `> .note` 사용
- `h3 + p`: 바로 다음 단락 이탤릭
- `h3 ~ p`: 이후 모든 형제 단락 상단 테두리

## 4. 페이지 구성

- `STEP 1`: 기본 선택자 실습
- `STEP 2`: 속성 선택자 실습
- `STEP 3`: 결합자 선택자 실습
- 스타일시트 적용 방법 요약 및 프로퍼티 예시 포함

---

<br/>
<br/>
<br/>

# CSS 타이포그래피 실습

## 1. 상속(Inheritance)

### 핵심 개념

- 텍스트 관련 속성(`color`, `font-family`, `font-size`, `line-height` 등)은 부모 → 자식 → 자손으로 **상속**됨.
- 박스 속성(`border`, `margin`, `padding`)은 상속되지 않음.
- 자식/자손에서 같은 속성을 다시 선언하면 조상의 값은 덮어써짐.

### 예시

```html
<div class="ancestor">
  조상 div → color: green; font-size: 18px
  <div class="child">
    자식 div → 조상 값 상속
    <div class="grandchild">손자 div → color: red; 로 덮어쓰기</div>
  </div>
</div>

<div class="ancestor-box">
  border 속성은 상속되지 않음
  <div class="child-box">→ 자식 div엔 border 없음</div>
</div>
```

## 2. 사이즈 단위

### 핵심 개념

- `px` : 절대 픽셀 단위. 화면 크기와 무관.
- `em` : 부모 `font-size` 기준 배수. 상속 체인 따라 누적됨.
- `rem` : `html` 기준 배수. 부모 영향 없음.
- `%` : 부모 대비 비율.

### 예시

```html
<p class="px">24px — 절대 크기</p>
<p class="em">2em — 부모의 2배</p>
<p class="rem">1.5rem — html 기준</p>
<p class="percent">120% — 부모 대비</p>
```

### em vs rem 비교

```html
<div class="parent" style="font-size: 20px;">
  부모 font-size: 20px
  <p class="child-em">2em → 20px * 2 = 40px</p>
  <p class="child-rem">2rem → html 16px * 2 = 32px</p>
</div>
```

---

## 3. 글꼴 속성(Font Properties)

### 핵심 개념

- `font-family` : 글꼴 계열 지정 (serif, sans-serif 등)
- `font-weight` : 글자 두께 (`normal`, `bold`, `100~900`)
- `font-style` : 기울임 (`italic`, `oblique`)
- `line-height` : 줄 간격
- `letter-spacing` : 글자 간격

### 예시

```html
<p class="font-family-serif">Georgia — 세리프 계열</p>
<p class="font-family-sans">Arial — 산세리프 계열</p>
<p class="weight-normal">font-weight: normal</p>
<p class="weight-bold">font-weight: bold</p>
<p class="weight-900">font-weight: 900</p>
<p class="italic">font-style: italic</p>
<p class="lineheight">line-height: 2</p>
<p class="spacing">letter-spacing: 4px</p>
```

---

## 4. 웹폰트(Web Font)

### 핵심 개념

- `@font-face` : 외부 폰트를 불러오는 규칙.
- CDN(Content Delivery Network)을 활용해 빠르게 제공 가능.
- 한국어 웹폰트는 눈누([noonnu.cc](https://noonnu.cc)) 등에서 쉽게 사용 가능.
- `body`에 지정해도 `input`, `textarea`, `button`에는 시스템 기본 폰트가 적용될 수 있어 별도 지정 필요.

### 예시

```css
@font-face {
  font-family: "PartialSansKR-Regular";
  src: url("https://fastly.jsdelivr.net/gh/projectnoonnu/noonfonts_2307-1@1.1/PartialSansKR-Regular.woff2")
    format("woff2");
  font-weight: normal;
  font-style: normal;
}

/* 적용 */
body.webfont {
  font-family: "PartialSansKR-Regular", sans-serif;
}
input,
textarea,
button {
  font-family: "PartialSansKR-Regular", sans-serif;
}
```

```html
<button onclick="document.body.classList.toggle('webfont')">웹폰트 토글</button>

<p>웹폰트 적용된 문장</p>
<input type="text" placeholder="input에도 적용됨" />
<textarea>textarea에도 적용됨</textarea>
<button>버튼에도 적용됨</button>
```

---
