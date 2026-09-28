# 김진웅 — Data Science & AI Research

Hugo로 만든 개인 연구자 포트폴리오·블로그 사이트입니다.

## 사이트 주소

https://qazcdesnu.github.io/qazcde-homepage/

GitHub Pages의 프로젝트 사이트이므로 `qazcdesnu.github.io` 아래 저장소 이름(`/qazcde-homepage/`) 하위 경로로 서비스됩니다. 커스텀 도메인은 연결되어 있지 않으며, `hugo.yaml`의 `baseURL`도 이 주소로 설정되어 있습니다.

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
