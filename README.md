# ia-codyssey
Github과 Codyssey 연동용

## 프로젝트 개요 (목표)
- 터미널 기본 조작 이해 (현재 위치 확인, 목록확인, 이동, 생성 복사, 이동/이름변경, 삭제 등)
- 권한 관리 학습
- Docker에 대한 기본적인 이해
- Docker 기반 이미지 제작
- 포트 매핑 및 접속 방법 숙지
- Docker 볼륨 영속성 검증
- Git 설정 및 GitHub 연동

## 1) 실행환경
- OS:
- 쉘/터미널: 
- Docker 버전:
- Git 버전:

## 2) 수행항목 체크리스트
- [x] 터미널 기본 조작
- [x] 파일 생성 및 수정
- [x] 권한 변경
- [x] Docker 설치
- [x] hello-world 실행
- [x] Dockerfile 빌드/실행
- [x] 포트 매핑 접속
- [x] 바인드 마운트 반영
- [x] 볼륨 영속성
- [x] Git 설정 + VScode GitHub 연동


## 3) 수행 로그 (검증 방법)
### 1) 터미널 조작 로그
```bash
pwd ## 현재 위치 확인
/Users/east####

ls -la ## ls: 목록 확인, -l: long format (자세히), -a: all(숨김 파일 포함) 
total 48
drwxr-x---+ 22 east#### east#### 704 Apr 2 12:09 . 
...

mkdir -p ~/dev/practice01 ## mkdir: 디렉토리 생성 -p: --parents 부모 디렉토리가 없으면 함께 만들어 줌
cd ~/dev/practice01 ## change directory 해당 디렉토리로 이동
pwd
/Users/east####/dev/practice01

touch hello.txt # hello.txt 파일 생성

echo 'Hello, Dev!' > hello.txt # 파일 내용 작성
cat hello.txt # 파일 내용 확인


```

### 2) Docker 운영/검증 로그
### 3) Dockerfile 기반 웹 서버 컨테이너
### 4) 포트 매핑 접속 증거
### 5) 바인드 마운트 반영 + 볼륨 영속성 증거
### 6) Git 설정 및 GitHub/VScode 연동 증거





## 4) 트러블 슈팅 (문제 -> 원인 -> 해결)



## 5) 핵심 개념 정리 목표

### 1) 절대경로와 상대경로의 차이
### 2) 파일 권한의 의미(r/w/x)와 755, 644 같은 표기의 이해
### 3) 기존 Dockerfile을 기반으로 "커스텀 이미지"를 만들 수 있는가
### 4) 포트 매핑이 필요한 이유
### 5) Docker 볼륨(영속 데이터) 설명
### 6) Git과 GitHub의 역할 차이(로컬 버전 관리 vs 원격 협업 플랫폼)

















