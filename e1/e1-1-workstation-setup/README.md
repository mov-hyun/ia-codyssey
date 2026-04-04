# E1-1. AI/SW 개발 워크스테이션 구축




## 프로젝트 개요
- [1. 터미널 기본 명령어](#1-터미널-기본-명령어--권한-부여)
- [2. Docker 기본 명령어](#2-docker-기본-명령어)
- [3. Docker 컨테이너 실습](#3-docker-컨테이너-실습)
- [4. Dockerfile 기반 커스텀 이미지 제작](#4-dockerfile-기반-커스텀-이미지-제작)
- [5. 포트 매핑](#5-포트-매핑)
- [6. 바인드 마운트 및 볼륨 영속성](#6-바인드-마운트-및-볼륨-영속성)
- [7. Git 설정 및 연동](#7-git-설정-및-연동)
- [8. Docker Compose](#8-docker-compose)
- [9. 트러블 슈팅](#9-트러블-슈팅)

------

#### 실행 환경

- OS:
- Shell:
- Docker version:
- Git version:

#### 수행항목 체크리스트

- [ ] 터미널 기본 조작 및 폴더 구성
- [ ] 권한 변경 실습
- [ ] Docker 설치/점검
- [ ] hello-world 실행
- [ ] Dockerfile 빌드/실행
- [ ] 포트 매핑 접속(2회)
- [ ] 바인드 마운트 반영
- [ ] 볼륨 영속성
- [ ] Git 설정 + VSCode GitHub 연동

------

### 1. 터미널 기본 명령어 / 권한 부여

#### 터미널 기본 명령어 정리

| 명령어 | 기능 | 사용 예시 | 설명 |
|--------|------|----------|------|
| `pwd` | 현재 디렉토리 경로 확인 | `pwd` | 현재 작업 중인 위치를 절대경로로 출력 |
| `ls` | 디렉토리 목록 확인 | `ls` | 현재 폴더 내 파일 및 디렉토리 출력 |
| `ls -la` | 숨김 파일 포함 상세 목록 | `ls -la` | 권한, 소유자, 크기 등 상세 정보 확인 |
| `cd` | 디렉토리 이동 | `cd practice/` | 특정 폴더로 이동 |
| `cd ..` | 상위 디렉토리 이동 | `cd ..` | 한 단계 위 폴더로 이동 |
| `mkdir` | 디렉토리 생성 | `mkdir test` | 새로운 폴더 생성 |
| `touch` | 파일 생성 | `touch file.txt` | 빈 파일 생성 |
| `cat` | 파일 내용 출력 | `cat file.txt` | 파일 내용을 터미널에 출력 |
| `echo` | 문자열 출력/파일 쓰기 | `echo "hi" > file.txt` | 파일에 내용 작성 |
| `cp` | 파일 복사 | `cp a.txt b.txt` | 파일 복제 |
| `mv` | 파일 이동/이름 변경 | `mv a.txt b.txt` | 파일 이름 변경 또는 이동 |
| `rm` | 파일 삭제 | `rm file.txt` | 파일 삭제 |
| `rm -r` | 디렉토리 삭제 | `rm -r folder` | 폴더 및 내부 파일 삭제 |

#### 현재 위치 확인

```bash
$ pwd
/Users/east0000/ia-codyssey/e1/e1-1-workstation-setup
```

#### 파일과 디렉토리 목록 확인

```bash
$ ls -la
사용자명@호스트명(혹은 ip주소)  e1-1-workstation-setup % ls -la
total 8 # 현재 디렉토리의 전체 용량: 8블록(8x512byte)
drwxr-xr-x  3 east0000  east0000    96 Apr  4 16:12 .
drwxr-xr-x  3 east0000  east0000    96 Apr  4 16:12 ..
-rw-r--r--  1 east0000  east0000  1618 Apr  4 17:55 README.md
```
첫 글자: 파일타입 d = 디렉토리, - = 일반 파일, l = 링크 r = read/4, w = write/2, x = execute/1    
1그룹: 소유자(Owner) 권한 2그룹: 그룹(Group) 권한 3그룹: 그 외 모든 사람(Others) 


### 2. Docker 기본 명령어


### 3. Docker 컨테이너 실습


### 4. Dockerfile 기반 커스텀 이미지 제작


### 5. 포트 매핑


### 6. 바인드 마운트 및 볼륨 영속성


### 7. Git 설정 및 연동


### 8. Docker Compose


### 9. 트러블 슈팅