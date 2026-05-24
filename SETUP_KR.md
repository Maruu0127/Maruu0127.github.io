# 포트폴리오 사이트 설정 · 배포 가이드

이 사이트는 [`luost26/academic-homepage`](https://github.com/luost26/academic-homepage) Jekyll 템플릿 기반입니다.
(참고하신 `jiankimr.github.io`와 동일한 템플릿) XMAD/XSANet 연구 맥락으로 초안이 채워져 있습니다.

---

## 1. 먼저 채워야 할 것 (`[TODO]` 표시 검색)

파일에서 `[TODO]` 를 검색하면 채울 곳이 모두 나옵니다.

| 파일 | 내용 |
|---|---|
| `_data/profile.yml` | 영문/한글 이름, 학위과정, 소속 연구실·대학, **GitHub 사용자명**, (선택) Google Scholar·LinkedIn·ORCID, 학력 |
| `_data/authors.yml` | `"Your Name"` → 본인 영문 이름 (논문 저자 bold 처리용) |
| `assets/images/photos/portrait.jpg` | 본인 프로필 사진으로 **파일 교체** |
| `_publications/2025/2025-xsanet.md` | XSANet 제목·저널·초록 확정 |
| `_publications/2026/2026-xmad.md` | (선택) 공저자·논문/코드 링크 추가 |
| `_config.yml` | `title` 의 이름, (선택) `url` |

> `profile.yml` 의 소셜 링크는 사용할 항목만 주석(`#`)을 해제하세요. 비워두면 표시되지 않습니다.

### 콘텐츠 추가/수정
- **논문 추가**: `_publications/<연도>/` 에 `.md` 파일 생성 (기존 파일 복사 후 수정). `selected: true` 면 홈 화면에도 노출.
- **프로젝트 추가**: `_showcase/projects/` 에 `.md` 파일 생성. `width` 는 1~12 (6이면 2열).
- **대표 이미지**: `assets/images/covers/` 에 넣고 각 파일의 `cover:` / `data-src` 경로 수정.

---

## 2. 로컬 미리보기 (선택)

```bash
bundle install            # 최초 1회 (이미 설치됨)
bundle exec jekyll serve  # http://127.0.0.1:4000 접속
```

> 참고: 이 환경의 시스템 Ruby(2.6)와 호환을 위해 `Gemfile` 에 `ffi` 버전 핀이 추가돼 있습니다.
> GitHub Pages 빌드에는 영향이 없습니다.

---

## 3. GitHub Pages 배포

### 3-1. GitHub에 저장소 생성
- 저장소 이름은 **반드시** `<본인-GitHub-사용자명>.github.io` 로 생성합니다.
  (예: 사용자명이 `gildong` 이면 → `gildong.github.io`)
- 비어 있는(README 없는) public 저장소로 만드세요.

### 3-2. 코드 푸시
이 폴더에서 (이미 `git init` + 첫 커밋이 되어 있습니다):

```bash
git remote add origin https://github.com/<사용자명>/<사용자명>.github.io.git
git branch -M main
git push -u origin main
```

### 3-3. Pages 활성화
1. GitHub 저장소 → **Settings → Pages**
2. **Build and deployment → Source** 를 **Deploy from a branch** 로 설정
3. Branch: **main**, 폴더: **/ (root)** → **Save**
4. 1~2분 뒤 `https://<사용자명>.github.io` 접속

> 개인 사이트(`username.github.io`)이므로 `_config.yml` 의 `baseurl` 은 빈 문자열(`""`)이 맞습니다. 그대로 두세요.

---

## 4. 자주 막히는 부분
- **CSS가 깨져 보임** → `baseurl` 이 `""` 인지 확인 (개인 사이트 기준).
- **이미지가 안 뜸** → 경로가 `/assets/...` 로 시작하는지 확인.
- **변경이 반영 안 됨** → 푸시 후 GitHub Actions 빌드가 끝나길 1~2분 대기.
