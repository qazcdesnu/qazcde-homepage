# 김진웅 — Data Science & AI Research

Hugo로 만든 개인 연구자 포트폴리오·블로그 사이트입니다.

## 로컬 실행

```bash
hugo server -D
```

## 정적 빌드

```bash
hugo --minify
```

생성된 정적 파일은 `public/` 디렉터리에 만들어집니다. GitHub Pages 배포는 `.github/workflows/hugo.yml`이 담당합니다.

프로젝트의 폴더 역할과 콘텐츠 작성 규칙은 [ARCHITECTURE.md](ARCHITECTURE.md)에 정리되어 있습니다.
