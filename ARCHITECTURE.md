# 사이트 아키텍처

## 1. 목표

김진웅님의 개인 연구자 포트폴리오와 기술 블로그를 하나의 정적 사이트로 운영한다.

- 정적 HTML 중심으로 빠르게 제공
- 블로그 글은 Markdown 파일로 작성
- 연구자 홈페이지에 어울리는 고전적이고 차분한 시각 언어 사용
- 데스크톱에서는 상단 네비게이션과 2단 콘텐츠 레이아웃 사용
- 모바일에서는 콘텐츠를 한 열로 자연스럽게 쌓음
- GitHub Pages의 GitHub Actions 배포를 통해 `main` 브랜치 push마다 자동 반영

## 2. 선택한 기술

- **Hugo**: Go 기반 정적 사이트 생성기
- **Markdown**: 블로그, 연구, 소개 콘텐츠 작성
- **Go HTML templates**: 공통 레이아웃과 페이지 템플릿
- **일반 CSS**: 외부 UI 프레임워크 없이 빠르고 오래 유지되는 스타일
- **GitHub Pages**: `public/` 정적 출력물 호스팅

브라우저에서 실행되는 필수 JavaScript는 사용하지 않는다. 모바일 메뉴도 CSS가 자연스럽게 줄바꿈하도록 구성해 초기 사이트를 단순하게 유지한다.

## 3. 폴더 구조

```text
.
├── archetypes/
│   └── blog.md                 # 새 블로그 글의 기본 front matter
├── content/
│   ├── _index.md               # 홈페이지 소개 문구
│   ├── about/_index.md         # 자기소개
│   ├── research/_index.md      # 연구 관심 분야
│   ├── publications/_index.md  # 논문 목록
│   ├── blog/
│   │   └── _index.md           # 블로그 목록 소개
│   └── cv/_index.md            # CV 안내
├── layouts/
│   ├── _default/
│   │   ├── baseof.html         # 모든 페이지의 HTML 골격
│   │   ├── list.html            # 일반 목록/섹션 페이지
│   │   └── single.html          # 일반 단일 페이지
│   ├── blog/
│   │   ├── list.html            # 블로그 목록
│   │   └── single.html          # 블로그 글 본문
│   ├── 404.html                 # 존재하지 않는 페이지
│   ├── index.html               # 홈페이지
│   └── partials/
│       ├── footer.html          # 공통 footer
│       ├── head.html            # 메타 태그와 CSS
│       ├── header.html          # 이름과 상단 네비게이션
│       ├── post-card.html       # 블로그 글 카드
│       └── sidebar.html         # 연구 관심 분야와 링크
├── static/
│   └── css/main.css             # 정적 스타일시트
├── .github/workflows/
│   └── hugo.yml                 # GitHub Pages 자동 배포
├── hugo.yaml                    # 사이트 설정, 메뉴, 기본 정보
└── ARCHITECTURE.md              # 이 문서
```

## 4. 페이지 역할

| 경로 | 역할 |
| --- | --- |
| `/` | 이름, 소속, 연구 관심 분야, 최근 글을 보여주는 첫 화면 |
| `/about/` | 짧은 자기소개와 연구자로서의 방향 |
| `/research/` | LLM, 생성형 AI, 데이터사이언스 관심 분야 |
| `/publications/` | 논문과 발표 목록을 추가할 자리 |
| `/blog/` | Markdown 글 목록 |
| `/blog/<slug>/` | 개별 글 본문 |
| `/cv/` | CV 파일과 경력 정보를 추가할 자리 |

## 5. 블로그 글 작성 규칙

새 글은 다음 명령으로 시작한다.

```bash
hugo new content/blog/my-first-note.md
```

생성된 파일은 다음과 같은 front matter를 가진다.

```yaml
---
title: "글 제목"
date: 2026-09-23
draft: true
summary: "목록에 표시할 짧은 요약"
tags: ["LLM", "Research"]
---
```

초안은 `draft: true`로 작성하고, 게시할 때 `draft: false`로 변경한다.

## 6. 배포 흐름

1. `main` 브랜치에 변경 사항을 push한다.
2. GitHub Actions가 Hugo를 설치하고 `hugo --minify`를 실행한다.
3. 생성된 `public/`을 GitHub Pages artifact로 업로드한다.
4. GitHub Pages가 artifact를 사이트로 배포한다.

저장소의 **Settings → Pages → Source**는 `GitHub Actions`로 설정해야 한다.

## 7. 유지보수 원칙

- 개인 정보와 링크는 `hugo.yaml`의 `params`에서 관리한다.
- 반복되는 HTML은 `layouts/partials/`에 둔다.
- 글 내용과 페이지 구조를 분리한다.
- 외부 폰트, UI 프레임워크, 불필요한 JavaScript는 추가하지 않는다.
- 디자인 토큰은 `static/css/main.css` 상단의 `:root`에서 먼저 조정한다.
