# 이서영 개인 소개 웹사이트 Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** 이서영(인천대학교 안전공학과)의 개인 소개 웹사이트를 순수 HTML/CSS/JS로 만들어 `inuprogram` 저장소에서 GitHub Pages 프로젝트 페이지로 배포한다.

**Architecture:** 빌드 도구 없는 정적 사이트. `index.html` 한 페이지에 상단 고정 네비게이션 + 4개 섹션(Home/About/Hobby/Contact)을 앵커 스크롤로 연결한다. 스타일은 `css/style.css` 한 파일, 동작은 `js/main.js` 한 파일(모바일 메뉴 토글 전용)로 분리한다.

**Tech Stack:** HTML5, CSS3(커스텀 프로퍼티, 미디어쿼리), Vanilla JavaScript(ES6). 외부 의존성은 Pretendard 폰트 CDN 하나뿐.

## Global Constraints

- 순수 HTML/CSS/JS만 사용한다. 빌드 도구, 프레임워크, 패키지 매니저를 도입하지 않는다.
- 외부 의존성은 Pretendard 가변 폰트 CDN(`https://cdn.jsdelivr.net/gh/orioncactus/pretendard@v1.3.9/dist/web/variable/pretendardvariable.css`) 하나만 허용한다.
- 반응형 브레이크포인트는 `768px` 단일 기준으로 한다 (그 이하 = 모바일).
- 색상 토큰: 배경 `#FFFFFF`, 기본 텍스트 `#1A1A1A`, 보조 텍스트 `#6B7280`, 포인트 컬러 `#0D9488`(teal-600), 구분선 `#E5E7EB`.
- JavaScript의 역할은 모바일 햄버거 메뉴 열기/닫기 토글로 한정한다. 그 외 애니메이션·효과는 추가하지 않는다.
- 자기소개(About)와 연락처(Contact)는 실제 내용이 아직 미정이므로 플레이스홀더 문구를 넣고, 각 자리에 `<!-- 실제 ○○로 교체 필요 -->` HTML 주석을 남긴다.
- 저장소 경로: `C:\Users\jkaa0\inuprogram` (remote: `https://github.com/jkaa0909-stack/inuprogram.git`, branch `main`). `inu-llm-lecture` 저장소는 이 작업에서 건드리지 않는다.

---

### Task 1: 저장소 스캐폴딩 + 기본 HTML 골격

**Files:**
- Create: `index.html`
- Create: `css/style.css` (스텁)
- Create: `js/main.js` (스텁)
- Create: `assets/.gitkeep`

**Interfaces:**
- Produces: `index.html`의 섹션 id(`home`, `about`, `hobby`, `contact`)와 nav 토글 요소 id(`navToggle`, `navMenu`) — Task 2~5에서 CSS 셀렉터와 JS `getElementById` 대상으로 그대로 사용한다.

- [ ] **Step 1: 아직 파일이 없는지 확인**

Run: `cd "c:\Users\jkaa0\inuprogram" && ls index.html css js 2>&1`
Expected: `No such file or directory` (index.html, css, js 모두 없음)

- [ ] **Step 2: 폴더 구조 생성**

```bash
cd "c:\Users\jkaa0\inuprogram"
mkdir css js assets
touch assets/.gitkeep
```

- [ ] **Step 3: `index.html` 작성**

```html
<!DOCTYPE html>
<html lang="ko">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>이서영 | 인천대학교 안전공학과</title>
  <meta name="description" content="이서영 - 인천대학교 안전공학과. 개인 소개 페이지입니다." />
  <link rel="stylesheet" href="https://cdn.jsdelivr.net/gh/orioncactus/pretendard@v1.3.9/dist/web/variable/pretendardvariable.css" />
  <link rel="stylesheet" href="css/style.css" />
</head>
<body>
  <header class="nav" id="nav">
    <div class="nav__inner">
      <a href="#home" class="nav__logo">이서영</a>
      <button type="button" class="nav__toggle" id="navToggle" aria-label="메뉴 열기" aria-expanded="false" aria-controls="navMenu">
        <span class="nav__toggle-bar"></span>
        <span class="nav__toggle-bar"></span>
        <span class="nav__toggle-bar"></span>
      </button>
      <nav class="nav__menu" id="navMenu">
        <a href="#home" class="nav__link">Home</a>
        <a href="#about" class="nav__link">About</a>
        <a href="#hobby" class="nav__link">Hobby</a>
        <a href="#contact" class="nav__link">Contact</a>
      </nav>
    </div>
  </header>

  <main>
    <section id="home" class="hero">
      <p class="hero__eyebrow">Hello, I'm</p>
      <h1 class="hero__name">이서영</h1>
      <p class="hero__affiliation">인천대학교 안전공학과</p>
    </section>

    <section id="about" class="section about">
      <h2 class="section__title">About</h2>
      <!-- 실제 자기소개로 교체 필요 -->
      <p class="about__text">
        안녕하세요, 인천대학교 안전공학과에 재학 중인 이서영입니다.
        사람과 현장을 더 안전하게 만드는 일에 관심이 많습니다.
      </p>
    </section>

    <section id="hobby" class="section hobby">
      <h2 class="section__title">Hobby</h2>
      <div class="hobby__card">
        <span class="hobby__icon" aria-hidden="true">&#127925;</span>
        <h3 class="hobby__name">음악듣기</h3>
        <p class="hobby__desc">다양한 장르의 음악을 들으며 휴식을 취하는 것을 좋아합니다.</p>
      </div>
    </section>

    <section id="contact" class="section contact">
      <h2 class="section__title">Contact</h2>
      <!-- 실제 연락처로 교체 필요 -->
      <ul class="contact__list">
        <li class="contact__item">
          <span class="contact__label">Email</span>
          <a href="mailto:example@inu.ac.kr" class="contact__value">example@inu.ac.kr</a>
        </li>
        <li class="contact__item">
          <span class="contact__label">Phone</span>
          <a href="tel:010-0000-0000" class="contact__value">010-0000-0000</a>
        </li>
      </ul>
    </section>
  </main>

  <footer class="footer">
    <p>&copy; 2026 이서영. All rights reserved.</p>
  </footer>

  <script src="js/main.js"></script>
</body>
</html>
```

- [ ] **Step 4: 구조 검증 (grep)**

Run:
```bash
cd "c:\Users\jkaa0\inuprogram"
grep -c 'id="home"' index.html
grep -c 'id="about"' index.html
grep -c 'id="hobby"' index.html
grep -c 'id="contact"' index.html
grep -c 'id="navToggle"' index.html
grep -c 'id="navMenu"' index.html
grep -c 'css/style.css' index.html
grep -c 'js/main.js' index.html
```
Expected: 모든 명령이 `1`을 출력.

- [ ] **Step 5: CSS/JS 스텁 작성 (링크 깨짐 방지)**

`css/style.css`:
```css
/* 이서영 개인 소개 웹사이트 스타일 — Task 2에서 채움 */
```

`js/main.js`:
```js
// 모바일 메뉴 토글 — Task 5에서 채움
```

- [ ] **Step 6: 브라우저에서 확인**

`index.html`을 더블클릭하거나 브라우저에서 `file:///C:/Users/jkaa0/inuprogram/index.html` 열기.
Expected: 브라우저 탭 제목이 "이서영 | 인천대학교 안전공학과"로 표시되고, 스타일 없는 상태로 Home/About/Hobby/Contact 4개 섹션 텍스트가 순서대로 보인다. F12 콘솔에 에러 없음.

- [ ] **Step 7: 커밋**

```bash
cd "c:\Users\jkaa0\inuprogram"
git add index.html css/style.css js/main.js assets/.gitkeep
git commit -m "feat: 기본 HTML 골격과 프로젝트 구조 추가"
```

---

### Task 2: 디자인 토큰 + 리셋 + 상단 네비게이션 스타일

**Files:**
- Modify: `css/style.css`

**Interfaces:**
- Consumes: Task 1의 `index.html` 클래스명(`nav`, `nav__inner`, `nav__logo`, `nav__toggle`, `nav__toggle-bar`, `nav__menu`, `nav__link`)
- Produces: CSS 커스텀 프로퍼티(`--color-bg`, `--color-text`, `--color-text-muted`, `--color-accent`, `--color-border`, `--space-1`~`--space-7`, `--font-sans`) — Task 3~5에서 그대로 재사용한다.

- [ ] **Step 1: 리셋 + 디자인 토큰 추가**

`css/style.css`에 아래 내용 추가:
```css
/* 이서영 개인 소개 웹사이트 스타일 */

:root {
  --color-bg: #ffffff;
  --color-text: #1a1a1a;
  --color-text-muted: #6b7280;
  --color-accent: #0d9488;
  --color-border: #e5e7eb;

  --space-1: 8px;
  --space-2: 16px;
  --space-3: 24px;
  --space-4: 32px;
  --space-5: 48px;
  --space-6: 64px;
  --space-7: 96px;

  --font-sans: 'Pretendard Variable', Pretendard, -apple-system, BlinkMacSystemFont,
    system-ui, Roboto, 'Helvetica Neue', 'Segoe UI', 'Apple SD Gothic Neo',
    'Noto Sans KR', 'Malgun Gothic', sans-serif;

  --nav-height: 64px;
}

*,
*::before,
*::after {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

html {
  scroll-behavior: smooth;
  scroll-padding-top: var(--nav-height);
}

body {
  font-family: var(--font-sans);
  color: var(--color-text);
  background: var(--color-bg);
  line-height: 1.6;
  -webkit-font-smoothing: antialiased;
}

a {
  color: inherit;
  text-decoration: none;
}

ul {
  list-style: none;
}
```

- [ ] **Step 2: 네비게이션 바 스타일 추가**

`css/style.css` 끝에 추가:
```css
.nav {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  height: var(--nav-height);
  background: var(--color-bg);
  border-bottom: 1px solid var(--color-border);
  z-index: 100;
}

.nav__inner {
  max-width: 960px;
  height: 100%;
  margin: 0 auto;
  padding: 0 var(--space-3);
  display: flex;
  align-items: center;
  justify-content: space-between;
}

.nav__logo {
  font-weight: 700;
  font-size: 1.125rem;
}

.nav__menu {
  display: flex;
  gap: var(--space-4);
}

.nav__link {
  font-size: 0.95rem;
  color: var(--color-text-muted);
  transition: color 0.15s ease;
}

.nav__link:hover {
  color: var(--color-accent);
}

.nav__toggle {
  display: none;
  flex-direction: column;
  justify-content: center;
  gap: 4px;
  width: 32px;
  height: 32px;
  background: none;
  border: none;
  cursor: pointer;
}

.nav__toggle-bar {
  width: 100%;
  height: 2px;
  background: var(--color-text);
}

main {
  padding-top: var(--nav-height);
}
```

- [ ] **Step 3: 브라우저에서 확인**

`file:///C:/Users/jkaa0/inuprogram/index.html`을 새로고침.
Expected: 상단에 흰 배경 + 하단 얇은 회색 선의 고정 네비게이션 바가 보이고, "이서영" 로고와 4개 메뉴가 가로로 정렬되어 있다. 메뉴에 마우스를 올리면 글자색이 청록색(`#0D9488`)으로 바뀐다. 페이지 텍스트 전체가 Pretendard 폰트(둥근 고딕 느낌)로 보인다 — Chrome DevTools Network 탭에서 `pretendardvariable.css` 요청이 200으로 로드됐는지 확인.

- [ ] **Step 4: 커밋**

```bash
cd "c:\Users\jkaa0\inuprogram"
git add css/style.css
git commit -m "style: 디자인 토큰과 상단 네비게이션 스타일 추가"
```

---

### Task 3: Hero + About 섹션 스타일

**Files:**
- Modify: `css/style.css`

**Interfaces:**
- Consumes: Task 2의 커스텀 프로퍼티(`--color-*`, `--space-*`, `--nav-height`)와 `index.html`의 `hero`, `hero__eyebrow`, `hero__name`, `hero__affiliation`, `section`, `about` 클래스

- [ ] **Step 1: Hero 섹션 스타일 추가**

`css/style.css` 끝에 추가:
```css
.hero {
  min-height: calc(100vh - var(--nav-height));
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  text-align: center;
  padding: var(--space-5) var(--space-3);
}

.hero__eyebrow {
  color: var(--color-accent);
  font-weight: 600;
  letter-spacing: 0.04em;
  margin-bottom: var(--space-2);
}

.hero__name {
  font-size: clamp(2.5rem, 6vw, 4rem);
  font-weight: 800;
  letter-spacing: -0.02em;
  margin-bottom: var(--space-2);
}

.hero__affiliation {
  color: var(--color-text-muted);
  font-size: clamp(1rem, 2vw, 1.25rem);
}
```

- [ ] **Step 2: 공용 섹션 + About 스타일 추가**

`css/style.css` 끝에 추가:
```css
.section {
  max-width: 640px;
  margin: 0 auto;
  padding: var(--space-7) var(--space-3);
}

.section__title {
  font-size: 1.75rem;
  font-weight: 700;
  margin-bottom: var(--space-4);
  text-align: center;
}

.about__text {
  color: var(--color-text);
  font-size: 1.05rem;
  line-height: 1.8;
  text-align: center;
}
```

- [ ] **Step 3: 브라우저에서 확인**

`index.html` 새로고침.
Expected: Home 섹션이 화면 높이 대부분을 차지하며 "Hello, I'm"(청록색 작은 글씨) → "이서영"(매우 큰 굵은 글씨) → "인천대학교 안전공학과"(회색 중간 글씨) 순으로 세로 중앙 정렬되어 보인다. 아래로 스크롤하면 About 섹션이 가운데 정렬된 좁은 폭의 문단으로 보인다.

- [ ] **Step 4: 커밋**

```bash
cd "c:\Users\jkaa0\inuprogram"
git add css/style.css
git commit -m "style: Hero, About 섹션 스타일 추가"
```

---

### Task 4: Hobby + Contact + Footer 섹션 스타일

**Files:**
- Modify: `css/style.css`

**Interfaces:**
- Consumes: Task 2~3의 토큰과 `index.html`의 `hobby__card`, `hobby__icon`, `hobby__name`, `hobby__desc`, `contact__list`, `contact__item`, `contact__label`, `contact__value`, `footer` 클래스

- [ ] **Step 1: Hobby 카드 스타일 추가**

`css/style.css` 끝에 추가:
```css
.hobby__card {
  border: 1px solid var(--color-border);
  border-radius: 12px;
  padding: var(--space-5);
  text-align: center;
}

.hobby__icon {
  display: inline-block;
  font-size: 2.5rem;
  margin-bottom: var(--space-2);
}

.hobby__name {
  font-size: 1.25rem;
  font-weight: 700;
  margin-bottom: var(--space-1);
}

.hobby__desc {
  color: var(--color-text-muted);
}
```

- [ ] **Step 2: Contact 리스트 스타일 추가**

`css/style.css` 끝에 추가:
```css
.contact__list {
  display: flex;
  flex-direction: column;
  gap: var(--space-2);
}

.contact__item {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: var(--space-2) var(--space-3);
  border: 1px solid var(--color-border);
  border-radius: 8px;
}

.contact__label {
  color: var(--color-text-muted);
  font-size: 0.9rem;
}

.contact__value {
  font-weight: 600;
  transition: color 0.15s ease;
}

.contact__value:hover {
  color: var(--color-accent);
}
```

- [ ] **Step 3: Footer 스타일 추가**

`css/style.css` 끝에 추가:
```css
.footer {
  border-top: 1px solid var(--color-border);
  padding: var(--space-4) var(--space-3);
  text-align: center;
  color: var(--color-text-muted);
  font-size: 0.85rem;
}
```

- [ ] **Step 4: 브라우저에서 확인**

`index.html` 새로고침 후 끝까지 스크롤.
Expected: Hobby 섹션에 둥근 모서리 테두리 카드가 가운데 정렬되어 있고 음표 아이콘, "음악듣기" 제목, 설명 문구가 보인다. Contact 섹션에는 Email/Phone 행이 각각 테두리 박스로 구분되어 있고 값에 마우스를 올리면 청록색으로 바뀐다. 맨 아래 Footer에 옅은 회색 저작권 문구가 있다.

- [ ] **Step 5: 커밋**

```bash
cd "c:\Users\jkaa0\inuprogram"
git add css/style.css
git commit -m "style: Hobby, Contact, Footer 섹션 스타일 추가"
```

---

### Task 5: 반응형 + 모바일 햄버거 메뉴 동작

**Files:**
- Modify: `css/style.css`
- Modify: `js/main.js`

**Interfaces:**
- Consumes: `index.html`의 `#navToggle`, `#navMenu`, `.nav__link` / Task 2의 `.nav__menu`, `.nav__toggle` 클래스
- Produces: `nav__menu--open` CSS 클래스 — JS가 토글하고 CSS가 이 클래스 유무로 모바일 메뉴 표시 여부를 결정한다.

- [ ] **Step 1: 모바일 브레이크포인트 CSS 추가**

`css/style.css` 끝에 추가:
```css
@media (max-width: 768px) {
  .nav__toggle {
    display: flex;
  }

  .nav__menu {
    position: fixed;
    top: var(--nav-height);
    right: 0;
    height: calc(100vh - var(--nav-height));
    width: 220px;
    background: var(--color-bg);
    border-left: 1px solid var(--color-border);
    flex-direction: column;
    align-items: flex-start;
    gap: var(--space-3);
    padding: var(--space-4) var(--space-3);
    transform: translateX(100%);
    transition: transform 0.2s ease;
  }

  .nav__menu--open {
    transform: translateX(0);
  }

  .hero__name {
    font-size: 2.5rem;
  }
}
```

- [ ] **Step 2: `js/main.js` 작성**

```js
const navToggle = document.getElementById('navToggle');
const navMenu = document.getElementById('navMenu');

navToggle.addEventListener('click', () => {
  const isOpen = navMenu.classList.toggle('nav__menu--open');
  navToggle.setAttribute('aria-expanded', String(isOpen));
});

navMenu.querySelectorAll('.nav__link').forEach((link) => {
  link.addEventListener('click', () => {
    navMenu.classList.remove('nav__menu--open');
    navToggle.setAttribute('aria-expanded', 'false');
  });
});
```

- [ ] **Step 3: 데스크톱 화면에서 회귀 확인**

`index.html`을 일반 브라우저 창(768px 초과 너비)에서 새로고침.
Expected: 햄버거 아이콘이 보이지 않고, Task 2에서 만든 가로 메뉴가 그대로 보인다.

- [ ] **Step 4: 모바일 화면에서 토글 동작 확인**

Chrome DevTools를 열고(F12) 기기 툴바(Ctrl+Shift+M)로 너비 375px 기기로 전환 후 새로고침.
Expected:
1. 가로 메뉴는 사라지고 오른쪽 상단에 3줄 햄버거 아이콘만 보인다.
2. 햄버거 아이콘 클릭 → 화면 오른쪽에서 메뉴 패널이 슬라이드되어 나타나고 Home/About/Hobby/Contact 4개 링크가 세로로 보인다. Elements 패널에서 `#navToggle`의 `aria-expanded` 속성이 `"true"`로 바뀐 것을 확인.
3. 메뉴 안의 링크(예: About) 클릭 → 해당 섹션으로 스크롤 이동하면서 메뉴 패널이 자동으로 닫힌다. `aria-expanded`가 다시 `"false"`로 바뀐 것을 확인.

- [ ] **Step 5: 커밋**

```bash
cd "c:\Users\jkaa0\inuprogram"
git add css/style.css js/main.js
git commit -m "feat: 모바일 반응형 및 햄버거 메뉴 토글 추가"
```

---

### Task 6: README 작성 + GitHub Pages 배포

**Files:**
- Create: `README.md`
- Modify: (없음, 배포 설정은 GitHub 저장소 설정에서 수행)

**Interfaces:**
- Consumes: 없음 (최종 배포 단계)

- [ ] **Step 1: `README.md` 작성**

```markdown
# 이서영 개인 소개 웹사이트

인천대학교 안전공학과 이서영의 개인 소개 페이지입니다.
순수 HTML/CSS/JavaScript로 제작되었으며 빌드 도구를 사용하지 않습니다.

## 로컬에서 보기

`index.html` 파일을 브라우저로 열면 바로 확인할 수 있습니다. 별도의 서버나 설치 과정이 필요 없습니다.

## 배포

GitHub Pages 프로젝트 페이지로 배포됩니다: https://jkaa0909-stack.github.io/inuprogram/

## 폴더 구조

\`\`\`
inuprogram/
├── index.html
├── css/
│   └── style.css
├── js/
│   └── main.js
└── assets/
\`\`\`
```

- [ ] **Step 2: 커밋**

```bash
cd "c:\Users\jkaa0\inuprogram"
git add README.md
git commit -m "docs: README 추가"
```

- [ ] **Step 3: GitHub에 push**

```bash
cd "c:\Users\jkaa0\inuprogram"
git push origin main
```
Expected: `main -> main` push 성공 메시지. (실행 전 사용자에게 push 여부 확인)

- [ ] **Step 4: GitHub Pages 활성화**

GitHub 저장소 페이지(`https://github.com/jkaa0909-stack/inuprogram`) → Settings → Pages 이동.
"Build and deployment" → Source를 `Deploy from a branch`로, Branch를 `main` / `/ (root)`로 설정 후 Save.
Expected: 페이지 상단에 "Your site is live at https://jkaa0909-stack.github.io/inuprogram/" 메시지가 몇 분 내로 표시됨.

- [ ] **Step 5: 배포 확인**

브라우저에서 `https://jkaa0909-stack.github.io/inuprogram/` 접속.
Expected: 로컬에서 확인한 것과 동일한 페이지가 실제 URL에서 정상적으로 보인다. 네비게이션 스크롤, 모바일 햄버거 메뉴 모두 정상 동작.

---

## 남은 작업 (이 계획 범위 밖)

- About의 실제 자기소개 문구, Contact의 실제 이메일/전화번호로 교체 (현재 플레이스홀더 + HTML 주석으로 표시되어 있음)
