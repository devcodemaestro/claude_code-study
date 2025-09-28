## 클로드코드 설치(WIN)

WSL2(Window Subsystem for Linux)를 구성한다.

1. Windows PowerShell을 관리자 권한으로 실행한다.

2. 터미널에 Linux용 Windows 하위 시스템과 VVirtual Machine Platform 기능을 활성화 한다.

```bash
dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all/ norestart
```

```bash
dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all/ norestart
```

작업을 완료 후 제어판>프로그램>프로그램 및 기능>Windows 기능 켜기/끄기 에서 Linux용 Windows 하위 시스텝 과 Virtual Machine Platform(가상머신 플랫폼)이 활성화 되어 있는 것을 확인한다.

3. 설정 변경이 있었다면 윈도우 시스템을 다시 시작한다. CPU의 가상화 기능이 활성화 되어 있지 않다면, 다시 시작하는 과정에서 활성화 시켜야 한다.

```bash
Restart-Computer
```

4. SWL2를 설치 및 업데이트하고, 기본 값으로 설정한다.

```bash
wsl --update

wsl --set-default-version 2
```

5. wsl --list --online으로 설치 가능한 가상 머신을 확인한다. 이 중 가장 최근의 LTS 버전을 설치하면 됨.

```bash
wsl --install Ubuntu-24.04
```

6.  설치 완료 후 사용자 이름과 이이디 입력시 모두 claude로 입력한다.

7.  윈도우 검색에서 Ubuntu를 검색해서 관리자 권한으로 실행한다.

8.  [Node.js 내려받기 화면](https:/nodejs.org/ko/download)으로 이동 후 for Linux using nvm with npm(리눅스 환경에서 nvm 방식으로 npm)을 선택하고 Copy to clipboard를 누른다.

9.  우분투 터미널에서 복사한 내용을 붙여넣어 Node.js를 설치한다.

- 이 때 npm -v와 node -v로 정상 출력을 확인한다.

10. 클로드코드를 설치한다.

```bash
npm install -g @anthropic-ai/claude-code
```

## 클로드 코드 최초 실행

1. 우분투 환경에서 claude를 입력한다.

2. 터미널의 테마를 선택한다. 기본값은 1. DarkMode다.

3. Claude account with subscription을 선택해 계정 연동을 진행한다.

4. 기본 설정을 진행하게 되는데 첫 화면은 약관과 같은 내용이고, 두번째 화면은 터미널 설정으로 Yes, use recommended settings를 누른다.

5. 현재 폴더를 신뢰할 수 있는지 확인요청이 나타나고, Yes, proceed를 눌러 계속 진행한다.

6. 설정이 완료되면 /doctor 명령을 입력해 클로드 코드를 점검한다.

7. /exit 명령을 입력해 나온 후에 다시 claude를 입력해서 설정 과정이 반복되지 않는 것을 확인한다.

## 클로드코드 내장 명령어

1. /를 입력하면 내장 명령어 예시가 나타난다. 또는 /help를 입력하면 다양한 프롬프트와 설명이 같이 나타난다.

2. !를 입력하면 claude 모드에서 bash 터미널 모드로 바뀐다. 예를들어 !를 입력한 후에 pwd를 입력하면 현재 디렉터리 위치를 확인할 수 있다.

3. claude 상태에서 궁금한 사항은 입력창에 물어보면 클로드 코드가 대답한다. 모르는 부분은 클로드코드에 바로바로 질문하도록 한다.

## 내 컴퓨터의 정보 분석하기

- 클로드 코드와 같은 인공지능 에이전트의 가장 큰 장점은 현재 시스템의 정보를 읽을 수 있다는 것이다.

- 하드웨어 정보, 운영 체제 정보 등을 물어보면 클로드 코드는 컴퓨터 내의 시스템 정보를 확인해 답변해준다.

- 또한 로컬 파일들을 손십게 분석하고 계산할 수 있다. 일일이 열어볼 필요없이 파일의 내용을 확인요청하거나 여러 피일의 내용들을 합쳐서 문의해도 확인 후 답변해준다.

- 특정한 폴더를 분석요청하거나 학습계획을 작성요청시에도 일정을 계획해주며, 깃헙 저장소를 내려받거나 주소를 자체를 알려주고 파악 요청하면 파악 후 알려주기도 한다.

## 웹 페이지 만들기

- 디렉터리에 가이드가 되는 CLAUDE.md 파일을 준비하고 특정한 웹페이지를 생성하면 거기에 맞춰서 웹 페이지를 생성한다. [예시](./CLAUDE.md)

- 우분투 환경의 경우 로컬과 별개이기 때문에 깃헙 자격 증명과 사용자 정보를 우분투환경에 다시 저장해야 한다.

### WSL2에서 GitHub 연동 설정 방법

방법 Personal Access Token 사용

1단계: GitHub에서 토큰 생성

1. https://github.com/settings/tokens 접속
2. "Generate new token" → "Generate new token (classic)"
3. 토큰 이름: WSL2-Development
4. 만료일: 90 days 또는 No expiration
5. 권한 선택:

   - ✅ repo (전체 저장소 접근)
   - ✅ workflow (GitHub Actions)
   - ✅ write:packages (패키지 업로드)

6. "Generate token" 클릭
7. 토큰 복사 (한 번만 표시됨!)

2단계: WSL2에서 Git 설정

1. Git 사용자 정보 설정

git config --global user.name "username"
git config --global user.email "user@gmail.com"

2. Git 자격 증명 저장소 설정

git config --global credential.helper store

3단계: 첫 번째 push 시 토큰 입력
git push origin main

1. Username: 본인 username

2. Password: [위에서 생성한 토큰 붙여넣기]
