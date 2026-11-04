# 대화 뷰어

빌드 없는 정적 사이트입니다. 왼쪽에서 대화를 고르면 오른쪽에 본문이 표시됩니다.

- `index.html`: 화면
- `style.css`: 스타일
- `app.js`: 목록 조회, 대화 구분, Markdown 표시
- `conversations/`: 직접 추가하는 Markdown 파일
- `THIRD_PARTY_LICENSES.txt`: app.js에 포함한 Marked·DOMPurify의 라이선스 고지

## 로컬: Live Server

이 폴더를 VS Code로 열고 `index.html`에서 **Open with Live Server**를 선택하세요.
빌드·Python·목록 파일 생성 없이 실행됩니다. MD를 추가한 뒤 새로고침하면 반영됩니다.
Live Server의 폴더 목록 기능으로 파일명을 알아내며 하위 폴더와 한글 파일명도 지원합니다.
`conversations/` 안에는 `index.html`을 넣지 마세요. 폴더 목록 대신 그 파일이 열리게 됩니다.
HTML을 더블클릭해 여는 `file://` 방식은 지원하지 않습니다.

## GitHub Pages: 빌드 없이 배포

1. 이 폴더 안의 파일을 공개 레포지토리 루트에 올립니다.
2. Settings → Pages → Source에서 **Deploy from a branch**를 선택합니다.
3. Branch는 `main`, Folder는 **/(root)**로 설정하고 저장합니다.
4. 이후 `conversations/`에 MD 파일을 추가하고 커밋·푸시하면 됩니다.

별도 워크플로·빌드·dist 폴더가 필요 없습니다. 기존에 GitHub Actions로 설정했다면 반드시
배포 소스를 위와 같이 바꾸세요.

GitHub Pages에는 폴더 목록 기능이 없으므로 공개 GitHub API로 레포지토리의 파일 목록을
조회합니다. 기본 GitHub Pages 주소에서는 레포지토리를 자동으로 알아냅니다.
레포지토리 루트와 기본 브랜치를 배포하는 구성을 전제로 합니다.
커스텀 도메인을 사용한다면 `index.html`의 첫 줄 근처를 다음처럼 설정하세요.

```html
<html lang="ko" data-repository="소유자/레포지토리">
```

개인 토큰은 넣지 않습니다. GitHub의 비로그인 API 요청 제한(일반적으로 IP당 시간당 60회)을
넘으면 목록 조회가 일시적으로 실패할 수 있습니다. 목록은 페이지를 불러올 때 한 번 조회하며,
대화 선택은 추가 API 요청을 하지 않습니다. 비공개 레포지토리에는 이 방식이 적용되지 않습니다.
공개 API의 파일 목록과 Pages 배포 사이에 잠깐 차이가 생길 수 있으므로 푸시 후 배포가 끝나길 기다려주세요.

## Markdown과 외부 라이브러리

HTML·CSS·JS만으로 동작합니다. npm 설치나 패키지 빌드는 필요 없습니다.
Markdown을 제목·표·목록·코드 형태로 표시하기 위해 Marked 18.1.3을,
본문의 실행 가능한 HTML을 정리하기 위해 DOMPurify 3.4.17을 app.js에 포함했습니다.
CDN에서 스크립트를 내려받지 않습니다. 이 코드를 함께 배포하므로 라이선스 고지도 유지합니다.

`나:` / `AI:`를 발언으로 구분하며 코드 블록 안의 구분자는 무시합니다.
`(첨부파일)`은 파일명만 표시합니다. 역할 구분 없는 MD는 일반 문서로 표시합니다.
외부 이미지와 수식 전용 렌더링은 지원하지 않습니다. 공개 사이트에서는 대화 원본도 공개됩니다.
