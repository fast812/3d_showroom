# 3D Showroom (GitHub Pages) 운영 가이드

이 문서는 **3D Showroom 레포(HTML 뷰어 + GLB 모델)**를  
**GitHub Pages로 배포**하고, `models/`에 `.glb` 파일을 추가/관리해서  
외부(예: 카페24 상품상세 iframe)에서 사용하는 방법을 “처음부터 끝까지” 안내합니다.

> 코드(HTML/JS) 내용은 레포에 이미 있으므로, 여기서는 **설치/배포/운영 절차**만 설명합니다.  
> Windows / macOS 둘 다 안내합니다.

---

# 1) 준비물

- GitHub 계정
- Git(필수)
- VS Code(권장)
- `.glb` 3D 모델 파일들

---

# 2) Git 설치 (Git이 없을 때)

## 2.1 Windows

### (A) winget으로 설치 (가장 쉬움)
PowerShell(또는 VS Code 터미널)에서 아래 실행:

```powershell
winget install --id Git.Git -e

설치 후 VS Code를 완전히 종료했다가 다시 실행하고 확인:

git --version
(B) winget이 없으면(직접 설치)

Git for Windows 설치 프로그램을 설치

설치 중 옵션에서 아래가 선택되어 있어야 합니다:

Git from the command line and also from 3rd-party software (PATH 포함)

설치 후 VS Code를 재시작하고:

git --version
2.2 macOS

터미널에서 확인:

git --version

없으면 아래 실행(설치 안내가 뜹니다):

xcode-select --install

설치 후 다시 확인:

git --version
3) GitHub에서 레포 만들기

GitHub 로그인 → New repository

Repository name: 3d_showroom (권장)

Visibility: Public 권장 (Pages 공개 배포 목적)

Create repository

4) 내 PC에 레포 가져오기 (Clone)

아래는 “원하는 폴더로 이동(cd) → clone → 폴더 들어가기”까지 예시를 포함합니다.

 cd는 “폴더 이동” 명령입니다.

4.1 Windows (PowerShell) 예시
예시 1) 바탕화면에 projects 폴더 만들고 그 안에 클론
cd $env:USERPROFILE\Desktop
mkdir projects
cd projects
git clone https://github.com/fast812/3d_showroom.git
cd 3d_showroom
예시 2) C:\work 폴더에 클론
cd C:\work
git clone https://github.com/fast812/3d_showroom.git
cd 3d_showroom
4.2 macOS (Terminal) 예시
예시 1) 홈 폴더 아래 projects에 클론
cd ~
mkdir -p projects
cd projects
git clone https://github.com/fast812/3d_showroom.git
cd 3d_showroom
예시 2) 데스크탑에 클론
cd ~/Desktop
git clone https://github.com/fast812/3d_showroom.git
cd 3d_showroom
5) 기본 파일 구조(운영 기준)

레포는 아래 구조를 기준으로 운영합니다.

3d_showroom/
  index.html
  viewer.html
  models.json
  models/
    deer.glb
    wolf.glb
    bear.glb
    rabbit.glb

models/ 폴더: .glb 모델 파일 저장

models.json: 탭(모델 목록) 자동 생성/초기 모델 결정에 사용

6) 모델(.glb) 추가 방법 (예: tiger.glb)
6.1 models/ 폴더에 파일 추가

예: models/tiger.glb 파일을 넣습니다.

6.2 models.json에 항목 추가

models.json의 배열에 아래 항목을 추가합니다:

{ "name": "tiger", "file": "models/tiger.glb" }

JSON 문법 주의

마지막 항목 뒤에 ,(쉼표) 붙이면 오류가 날 수 있습니다.

대괄호 [ ] 구조 유지

6.3 커밋 & 푸시

Windows/macOS 공통:

git add .
git commit -m "Add tiger model"
git push
7) 로컬에서 미리 보기(권장)

파일을 더블클릭해서 file://로 열면 환경에 따라 GLB 로딩이 막힐 수 있습니다.
로컬 서버로 여는 방식을 권장합니다.

VS Code Live Server 사용(추천)

VS Code에서 3d_showroom 폴더 열기

Extensions에서 Live Server 설치

index.html 우클릭 → Open with Live Server

8) GitHub Pages 배포 켜기

레포(예: fast812/3d_showroom)에서:

Settings

왼쪽 메뉴 Pages

Source: Deploy from a branch

Branch: main / Folder: /(root)

Save

배포가 완료되면 Pages URL이 생성됩니다:

https://아이디.github.io/3d_showroom/

배포 반영에는 수십 초~수분 걸릴 수 있습니다.

9) 배포 URL 사용법 (모델별로 바로 열기)

특정 모델을 바로 띄우려면 URL 파라미터를 사용합니다.

형식:

https://아이디.github.io/3d_showroom/viewer.html?m=models/파일명.glb

예시:

deer
https://아이디.github.io/3d_showroom/viewer.html?m=models/deer.glb

wolf
https://아이디.github.io/3d_showroom/viewer.html?m=models/wolf.glb

bear
https://아이디.github.io/3d_showroom/viewer.html?m=models/bear.glb

rabbit
https://아이디.github.io/3d_showroom/viewer.html?m=models/rabbit.glb

10) 카페24 상품상세에 iframe으로 넣기

상품 상세(HTML 소스)에 아래처럼 삽입합니다.

<iframe
  src="https://아이디.github.io/3d_showroom/viewer.html?m=models/deer.glb"
  style="width:100%; height:700px; border:0; border-radius:12px;"
  loading="lazy">
</iframe>

모델만 바꾸려면 m=models/___ .glb 부분만 교체하면 됩니다.

11) 자주 발생하는 문제 / 해결
11.1 업데이트가 바로 반영되지 않음

GitHub Pages 배포 반영에 시간이 걸릴 수 있습니다.

브라우저 캐시 때문에 구버전이 보일 수 있어 강력 새로고침(Ctrl+F5) 권장

또는 URL 뒤에 임시로 ?v=2 같은 값을 붙여 캐시를 피할 수 있습니다.

11.2 특정 GLB에서 경고(재질 확장) 발생

일부 GLB는 구형 glTF 재질 확장(예: spec/gloss)을 포함해 경고가 날 수 있습니다.

해결: Blender에서 해당 GLB를 다시 export(재-export) 하면 호환성이 좋아집니다.

11.3 모델이 너무 크고 느림

폴리곤 수/텍스처 용량 최적화 후 업로드를 권장합니다.