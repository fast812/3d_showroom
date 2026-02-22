# 3D Showroom (GitHub Pages) 운영 가이드

이 문서는 **3D Showroom 레포(HTML 뷰어 + GLB 모델)**를  
**GitHub Pages로 배포**하고, `models/`에 `.glb` 파일을 추가/관리해서  
외부(예: 카페24 상품상세 iframe)에서 사용하는 방법을 “처음부터 끝까지” 안내합니다.

> 코드(HTML/JS) 내용은 레포에 이미 있으므로, 여기서는 **설치/배포/운영 절차**만 설명합니다.  
> Windows / macOS 둘 다 안내합니다.

---

## 1) 준비물

- GitHub 계정
- Git(필수)
- VS Code(권장)
- `.glb` 3D 모델 파일들

---

## 2) Git 설치 (Git이 없을 때)

### 2.1 Windows

#### (A) winget으로 설치 (가장 쉬움)
PowerShell(또는 VS Code 터미널)에서 아래 실행:

~~~powershell
winget install --id Git.Git -e
~~~

설치 후 **VS Code를 완전히 종료했다가 다시 실행**하고 확인:

~~~powershell
git --version
~~~

#### (B) winget이 없으면(직접 설치)
1) Git for Windows 설치 프로그램을 설치  
2) 설치 중 옵션에서 아래가 선택되어 있어야 합니다:

- **Git from the command line and also from 3rd-party software** (PATH 포함)

설치 후 VS Code를 재시작하고 확인:

~~~powershell
git --version
~~~

### 2.2 macOS

터미널에서 확인:

~~~bash
git --version
~~~

없으면 아래 실행(설치 안내가 뜹니다):

~~~bash
xcode-select --install
~~~

설치 후 다시 확인:

~~~bash
git --version
~~~

---

## 3) Git 사용자 정보 설정(처음 1회)

커밋을 하려면 Git에 사용자 이름/이메일이 등록되어 있어야 합니다.

### 3.1 Windows / macOS 공통
아래를 본인 정보로 바꿔서 1회 실행:

~~~bash
git config --global user.name "Your Name"
git config --global user.email "you@example.com"
~~~

확인:

~~~bash
git config --global user.name
git config --global user.email
~~~

> 이메일을 공개하기 싫다면 GitHub 설정(Settings → Emails)에서 제공하는  
> `...@users.noreply.github.com` 형식 이메일을 사용해도 됩니다.

---

## 4) fast812 템플릿을 내 레포로 업로드

> fast812 레포를 ZIP으로 받아서 내 GitHub 레포에 새로 올립니다.

### 4.1 내 GitHub에 새 레포 만들기
1) GitHub 로그인 → **New repository**  
2) Repository name: 예) `3d_showroom`  
3) Visibility: **Public** 권장 (Pages 공개 배포 목적)  
4) **Create repository**

### 4.2 fast812 템플릿 ZIP 다운로드
1) `https://github.com/fast812/3d_showroom` 접속  
2) **Code** 버튼 → **Download ZIP**  
3) ZIP 압축 해제 (예: `3d_showroom` 폴더가 생김)

### 4.3 VS Code로 폴더 열기
1) VS Code → **File → Open Folder…**  
2) 방금 압축 해제한 `3d_showroom` 폴더 선택  
3) VS Code 터미널 열기: **Terminal → New Terminal**

---

## 5) 내 레포로 최초 업로드(push)

> 아래 명령은 `3d_showroom` 폴더 안에서 실행해야 합니다.  
> (VS Code 터미널이 해당 폴더를 가리키는지 확인)

### 5.1 현재 위치 확인(선택)
~~~bash
pwd
~~~
- Windows PowerShell에서는 `pwd` 대신 아래도 가능:
~~~powershell
Get-Location
~~~

### 5.2 Git 초기화 + 커밋 + push
1) Git 초기화 및 커밋:

~~~bash
git init
git add .
git commit -m "Initial commit"
~~~

2) 브랜치를 main으로 맞추고, 내 레포를 origin으로 등록 후 push:

아래 URL은 **내 레포 주소로 바꿔서** 넣습니다.  
예) `https://github.com/내아이디/3d_showroom.git`

~~~bash
git branch -M main
git remote add origin https://github.com/내아이디/3d_showroom.git
git push -u origin main
~~~

> push 중 로그인/인증 창이 뜨면 GitHub 로그인을 진행하세요.

---

## 6) 기본 파일 구조(운영 기준)

레포는 아래 구조를 기준으로 운영합니다.

~~~text
3d_showroom/
  index.html
  viewer.html
  models.json
  models/
    deer.glb
    wolf.glb
    bear.glb
    rabbit.glb
~~~

- `models/` 폴더: `.glb` 모델 파일 저장
- `models.json`: 탭(모델 목록) 자동 생성/초기 모델 결정에 사용

---

## 7) 모델(.glb) 추가 방법 (예: tiger.glb)

### 7.1 `models/` 폴더에 파일 추가
예: `models/tiger.glb` 파일을 넣습니다.

### 7.2 `models.json`에 항목 추가
`models.json`의 배열에 아래 항목을 추가합니다:

~~~json
{ "name": "tiger", "file": "models/tiger.glb" }
~~~

> JSON 문법 주의  
> - 마지막 항목 뒤에 `,`(쉼표) 붙이면 오류가 날 수 있습니다.  
> - 대괄호 `[` `]` 구조를 유지하세요.

### 7.3 커밋 & 푸시
Windows/macOS 공통:

~~~bash
git add .
git commit -m "Add tiger model"
git push
~~~

---

## 8) GitHub Pages 배포 켜기

내 레포(예: `내아이디/3d_showroom`)에서:

1) **Settings**  
2) 왼쪽 메뉴 **Pages**  
3) Source: **Deploy from a branch**  
4) Branch: `main` / Folder: `/(root)`  
5) **Save**

배포가 완료되면 Pages URL이 생성됩니다:

- `https://내아이디.github.io/3d_showroom/`

> 배포 반영에는 수십 초~수분 걸릴 수 있습니다.

---

## 9) 배포 URL 사용법 (모델별로 바로 열기)

특정 모델을 바로 띄우려면 URL 파라미터를 사용합니다.

형식:
- `https://내아이디.github.io/3d_showroom/viewer.html?m=models/파일명.glb`

예시:
- deer: `https://내아이디.github.io/3d_showroom/viewer.html?m=models/deer.glb`
- wolf: `https://내아이디.github.io/3d_showroom/viewer.html?m=models/wolf.glb`
- bear: `https://내아이디.github.io/3d_showroom/viewer.html?m=models/bear.glb`
- rabbit: `https://내아이디.github.io/3d_showroom/viewer.html?m=models/rabbit.glb`

---

## 10) 카페24 상품상세에 iframe으로 넣기

상품 상세(HTML 소스)에 아래처럼 삽입합니다.

~~~html
<iframe
  src="https://내아이디.github.io/3d_showroom/viewer.html?m=models/deer.glb"
  style="width:100%; height:700px; border:0; border-radius:12px;"
  loading="lazy">
</iframe>
~~~

모델만 바꾸려면 `m=models/___ .glb` 부분만 교체하면 됩니다.

---

## 11) 자주 발생하는 문제 / 해결

### 11.1 업데이트가 바로 반영되지 않음
- GitHub Pages 배포 반영에 시간이 걸릴 수 있습니다.
- 브라우저 캐시 때문에 구버전이 보일 수 있어 **강력 새로고침(Ctrl+F5)** 권장
- 또는 URL 뒤에 임시로 `?v=2` 같은 값을 붙여 캐시를 피할 수 있습니다.

### 11.2 커밋에서 “Author identity unknown” 오류
- 3) Git 사용자 정보 설정을 먼저 했는지 확인하세요:
~~~bash
git config --global user.name
git config --global user.email
~~~

### 11.3 특정 GLB에서 경고(재질 확장) 발생
- 일부 GLB는 구형 glTF 재질 확장(예: spec/gloss)을 포함해 경고가 날 수 있습니다.
- 해결: Blender에서 해당 GLB를 다시 export(재-export)하면 호환성이 좋아집니다.

### 11.4 모델이 너무 크고 느림
- 폴리곤 수/텍스처 용량 최적화 후 업로드를 권장합니다.