# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

정적 HTML 단일 파일 포트폴리오 사이트. 빌드 도구, 패키지 매니저, 프레임워크 없이 브라우저에서 직접 열어 동작한다.

- **진입점**: `index.html` (전체 사이트가 이 하나의 파일에 포함됨)
- **스타일링**: Tailwind CSS CDN (`tailwind.config`는 파일 내 인라인으로 정의)
- **폰트**: Google Fonts CDN (Inter, Noto Sans KR, JetBrains Mono)
- **JS**: 외부 라이브러리 없음, 바닐라 JS만 사용

## 실행 방법

별도 빌드/설치 없음. `index.html`을 브라우저로 직접 열면 된다.

```bash
# Windows
start index.html

# 또는 Live Server (VS Code 확장) 사용 권장 — 저장 시 자동 새로고침
```

## 아키텍처

`index.html` 내부 구조:

| 영역 | 내용 |
|------|------|
| `<head>` | Tailwind CDN, `tailwind.config` (커스텀 색상/폰트), 인라인 CSS (keyframes, `.fade-in`, `.skill-bar-fill` 등) |
| `#hero` | 타이프라이터 효과, 그라디언트 애니메이션 배경 |
| `#about` | 프로필 카드 + 정보 카드 그리드 |
| `#skills` | 스킬 카드 3개 (COBOL 90%, HTML 85%, C 80%) — `data-width` 속성으로 바 너비 제어 |
| `#projects` | 프로젝트 카드 3개 (현재 모두 "준비중") |
| `#contact` | 이메일 CTA + GitHub/LinkedIn 아이콘 |
| `<script>` | 7개 기능 (모바일 메뉴, 헤더 스크롤, 활성 네비, 스킬 바, fade-in, 타이프라이터, 맨위로 버튼) |

## 커스텀 Tailwind 색상

```js
navy: {
  950: '#060d1f',  // 최어두운 배경
  900: '#0a1628',
  800: '#0f2040',
  700: '#1a3055',
  600: '#264473',
}
```
`navy-*` 클래스는 CDN Tailwind에 기본 포함되지 않으므로 `tailwind.config` 블록을 반드시 유지해야 한다.

## 주의사항

- 스킬 바 애니메이션은 `data-width` 속성값을 JS가 읽어 `style.width`에 적용하는 방식 (`index.html:601`)
- fade-in은 IntersectionObserver 기반으로, `.fade-in` 클래스에 `.visible`을 추가하는 방식 (`index.html:611`)
- 연락처 이메일이 `#about`(272번째 줄)과 `#contact`(492, 500번째 줄) 두 곳에 하드코딩되어 있음 — 변경 시 두 곳 모두 수정 필요
