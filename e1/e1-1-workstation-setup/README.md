# E1-1. AI/SW 개발 워크스테이션 구축




## 프로젝트 개요
- [1. 터미널 기본 명령어 & 권한 부여](#1-터미널-기본-명령어--권한-부여)
- [2. Docker 기본 명령어 & 실습](#2-docker-기본-명령어--실습)
- [3. Dockerfile 기반 커스텀 이미지 제작](#3-dockerfile-기반-커스텀-이미지-제작)
- [4. 포트 매핑](#4-포트-매핑)
- [5. 바인드 마운트 및 볼륨 영속성](#5-바인드-마운트-및-볼륨-영속성)
- [6. Git 설정 및 연동](#6-git-설정-및-연동)
- [7. Docker Compose](#7-docker-compose)
- [8. 트러블 슈팅](#8-트러블-슈팅)

------

### 실행 환경

- OS: Sequoia 15.7.4
- Shell: zsh
- Docker version: 28.5.2
- Git version:

### 수행항목 체크리스트

- [x] 터미널 기본 조작 및 폴더 구성
- [x] 권한 변경 실습
- [x] Docker 설치/점검
- [x] hello-world 실행
- [ ] Dockerfile 빌드/실행
- [ ] 포트 매핑 접속(2회)
- [ ] 바인드 마운트 반영
- [ ] 볼륨 영속성
- [ ] Git 설정 + VSCode GitHub 연동

------

## 1. 터미널 기본 명령어 & 권한 부여

### 1.1 터미널 기본 명령어 정리

| 명령어 | 기능 | 사용 예시 | 설명 |
|--------|------|----------|------|
| `pwd` | 현재 디렉토리 경로 확인 | `pwd` | 현재 작업 중인 위치를 절대경로로 출력 |
| `ls` | 디렉토리 목록 확인 | `ls` | list 현재 폴더 내 파일 및 디렉토리 출력 |
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

### 1.2 현재 위치 확인

```bash
$ pwd
/Users/east0000/ia-codyssey/e1/e1-1-workstation-setup
```

### 1.3 파일과 디렉토리 목록과 권한 확인

```bash
$ ls -la
사용자명@호스트명(혹은 ip주소)  e1-1-workstation-setup % ls -la
total 8 # 현재 디렉토리의 전체 용량: 8블록(8x512byte)
drwxr-xr-x  3 east0000  east0000    96 Apr  4 16:12 .
drwxr-xr-x  3 east0000  east0000    96 Apr  4 16:12 ..
-rw-r--r--  1 east0000  east0000  1618 Apr  4 17:55 README.md
```
- 첫 글자는 파일타입 `d` = 디렉토리, `-` = 일반 파일, `l` = 링크 `r` = read/4, `w` = write/2, `x` = execute/1    
- 1그룹: 소유자(Owner) 2그룹: 그룹(Group) 3그룹: 그 외 모든 사람(Others)   
- `ls`: 파일/폴더 이름만 표시, `-l`: 권한, 크기, 수정일 표시, `-a`: 숨김파일(`.`으로 시작) 표시, `-lh`: 파일 크기 kb, mb단위로 표시


### 1.4 디렉토리 생성 및 이동

```bash
east0000@0000 e1-1-workstation-setup % mkdir hi # hi 디렉토리 생성
east0000@0000 e1-1-workstation-setup % ls      # 디렉토리 생성 확인
hi              README.md
east0000@0000 e1-1-workstation-setup % cd hi   # 디렉토리 이동
east0000@0000 hi % pwd                         # 현재 위치 확인
/Users/east0000/ia-codyssey/e1/e1-1-workstation-setup/hi
```

### 1.5 파일 생성 및 내용 추가, 확인

```bash
east0000@0000 hi % touch hello.txt # 파일 생성
east0000@0000 hi % cat hello.txt   # 파일 내용 확인 -> 비어있음
east0000@0000 hi % echo "hello codyssey!" > hello.txt # 파일 내용 추가
dquote>    
east0000@0000 hi %   # !와 "가 붙어 히스토리 확장으로 잘못 해석 -> 자세한 내용 트러블 슈팅 항목 참고
east0000@0000 hi % echo 'hello codyssey!' > hello.txt # 큰따옴표(")를 작은따옴표(')로 교체해 해결
east0000@0000 hi % cat hello.txt # 파일 내용 확인
hello codyssey!
```

### 1.6 파일 복사, 이름 변경, 제거

```bash
east0000@0000 hi % cp hello.txt copy.txt # 파일 복사
east0000@0000 hi % ls # 리스트 확인
copy.txt        hello.txt
east0000@0000 hi % mv copy.txt renamed.txt # 파일 이름 변경
east0000@0000 hi % ls # 이름 변경 확인
hello.txt       renamed.txt
east0000@0000 hi % cd .. # 상위 디렉토리로 이동
east0000@0000 e1-1-workstation-setup % rm -r hi # 디렉토리 삭제
east0000@0000 e1-1-workstation-setup % ls # 삭제 확인
README.md
```
`rm` 파일삭제, `-r` 폴더삭제, `-f` 강제삭제, `-i` 삭제 전 확인

### 1.7 파일 권한 변경

```bash
east0000@0000 e1-1-workstation-setup % touch file.txt # 파일 생성
east0000@0000 e1-1-workstation-setup % ls -la # 파일 권한 확인
total 16
drwxr-xr-x  4 east0000  east0000   128 Apr  4 19:07 .
drwxr-xr-x  3 east0000  east0000    96 Apr  4 16:12 ..
-rw-r--r--  1 east0000  east0000     0 Apr  4 19:07 file.txt
-rw-r--r--  1 east0000  east0000  4798 Apr  4 18:48 README.md
east0000@0000 e1-1-workstation-setup % chmod 755 file.txt # 파일 권한 변경
east0000@0000 e1-1-workstation-setup % ls -la # 파일 권한 확인
total 16
drwxr-xr-x  4 east0000  east0000   128 Apr  4 19:07 .
drwxr-xr-x  3 east0000  east0000    96 Apr  4 16:12 ..
-rwxr-xr-x  1 east0000  east0000     0 Apr  4 19:07 file.txt
-rw-r--r--  1 east0000  east0000  4798 Apr  4 18:48 README.md
```

### 1.8 디렉토리 권한 변경

```bash
east0000@0000 e1-1-workstation-setup % mkdir test # 디렉토리 생성
east0000@0000 e1-1-workstation-setup % ls -ld test # 디렉토리 권한 확인(-d는 폴더 자체 정보만 표시)
drwxr-xr-x  2 east0000  east0000  64 Apr  4 19:14 test 
east0000@0000 e1-1-workstation-setup % chmod 700 test # 권한 변경
east0000@0000 e1-1-workstation-setup % ls -ld test # 권한 확인
drwx------  2 east0000  east0000  64 Apr  4 19:14 test
```
`u+x` 소유자에게 실행권한 추가, `g-w` 그룹에서 쓰기 권한 제거, `o=r` 다른사람 권한 읽기만으로 지정, `a+r` 모두에게 읽기 권한 추가      
`chmod -R 755 test` 폴더 안의 모든 파일/폴더까지 한 번에 변경

## 2. Docker 기본 명령어 & 실습

### 2.1 Docker 기본 명령어 정리

| 명령어 | 기능 | 사용 예시 | 설명 |
|--------|------|----------|------|
| `docker --version` | Docker 버전 확인 | `docker --version` | Docker CLI 설치 여부 및 버전 확인 |
| `docker info` | Docker 엔진 상태 확인 | `docker info` | Docker 데몬 실행 여부 및 시스템 정보 확인 |
| `docker images` | 이미지 목록 조회 | `docker images` | 로컬에 저장된 이미지 확인 |
| `docker pull` | 이미지 다운로드 | `docker pull ubuntu` | Docker Hub에서 이미지 가져오기 |
| `docker ps` | 실행 중 컨테이너 조회 | `docker ps` | 현재 실행 중인 컨테이너 확인 |
| `docker ps -a` | 전체 컨테이너 조회 | `docker ps -a` | 중지된 컨테이너 포함 전체 조회 |
| `docker run` | 컨테이너 실행 | `docker run ubuntu` | 이미지 기반으로 컨테이너 생성 및 실행 |
| `docker run -it` | 인터랙티브 실행 | `docker run -it ubuntu bash` | 터미널에서 직접 컨테이너 접근 |
| `docker run -d` | 백그라운드 실행 | `docker run -d nginx` | 컨테이너를 백그라운드로 실행 |
| `docker stop` | 컨테이너 중지 | `docker stop <컨테이너ID>` | 실행 중인 컨테이너 종료 |
| `docker rm` | 컨테이너 삭제 | `docker rm <컨테이너ID>` | 중지된 컨테이너 삭제 |
| `docker rmi` | 이미지 삭제 | `docker rmi <이미지ID>` | 로컬 이미지 삭제 |
| `docker logs` | 로그 확인 | `docker logs <컨테이너ID>` | 컨테이너 실행 로그 확인 |
| `docker stats` | 리소스 사용 확인 | `docker stats` | CPU, 메모리 등 사용량 확인 |


### 2.2 Docker 버전 및 상태 확인

 ```bash
east0000@c1111 e1-1-workstation-setup % docker --version # 도커 버전 확인
Docker version 28.5.2, build ecc6942
east0000@c1111 e1-1-workstation-setup % docker info # 도커 엔진 상태 확인
Client:
 Version:    28.5.2
 Context:    orbstack
 Debug Mode: false
 Plugins:
  buildx: Docker Buildx (Docker Inc.)
    Version:  v0.29.1
                    ----이하생략----
east0000@c1111 e1-1-workstation-setup % docker images # 이미지 목록 (현재 없음)
REPOSITORY   TAG       IMAGE ID   CREATED   SIZE
east0000@c1111 e1-1-workstation-setup % docker ps -a  # 컨테이너 목록 조회 (-a: 종료된 것 포함) (현재 없음)
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
```
- `docker info` 명령 시  
`Containers` 전체/실행 중/정지된 컨테이너 개수, `Images` 설치된 이미지 개수, `Server Version` Docker 엔진 버전, `Storage Driver` 사용 중인 스토리지 드라이버,   
`Logging Driver` 컨테이너 로그 저장 방식, `Cgroup Driver / Version` 리소스 제어 방식, `Plugins` 네트워크/볼륨/로그 플러그인 정보, `Swarm` Docker Swarm 활성화 여부,  
`Runtimes` 사용 가능한 컨테이너 런타임 정보, `Default Runtime` 기본 런타임, `OS / Architecture` 운영체제 및 CPU 아키텍처, `CPUs / Total Memory` 시스템 자원 정보,  
`Docker Root Dir` Docker 데이터 저장 위치, `Network` 브리지 등 네트워크 설정 정보

### 2.3 hello-world 실행

 ```bash
east0000@c1111 e1-1-workstation-setup % docker run hello-world # hello-world 실행
---생략---
Hello from Docker!
This message shows that your installation appears to be working correctly.
---생략---
east0000@c1111 e1-1-workstation-setup % docker ps -a # 컨테이너 실행 결과 확인
CONTAINER ID   IMAGE         COMMAND    CREATED         STATUS                     PORTS     NAMES
395f6b60557b   hello-world   "/hello"   3 minutes ago   Exited (0) 3 minutes ago             hungry_rosalind
```

### 2.4 Ubuntu 컨테이너 실행

 ```bash
east0000@c1111 e1-1-workstation-setup % docker run -it ubuntu bash # 우분투 컨테이너 실행 및 내부 진입(-it: 터미널 인터랙션, bash: 컨테이너 내부 쉘 실행)
Unable to find image 'ubuntu:latest' locally
latest: Pulling from library/ubuntu
...........
Status: Downloaded newer image for ubuntu:latest
root@1234:/# ls # 리눅스 명령어 사용가능
bin  boot  dev  etc  home  lib  lib64  media  mnt  opt  proc  root  run  sbin  srv  sys  tmp  usr  var
root@1234:/# echo "hello docker" 
hello docker
root@1234:/# exit # 컨테이너 종료 (bash 종료시 함께 종료)
exit
east0000@c1111 e1-1-workstation-setup % docker ps -a # 종료된 컨테이너 확인 *exited(0): 정상 종료 의미
CONTAINER ID   IMAGE         COMMAND    CREATED          STATUS                     PORTS     NAMES
1234   ubuntu        "bash"     27 seconds ago   Exited (0) 5 seconds ago             exciting_goldwasser
395f6b60557b   hello-world   "/hello"   6 minutes ago    Exited (0) 6 minutes ago             hungry_rosalind            hungry_rosalind
```

### 2.5 이미지와 컨테이너의 차이

#### Docker 이미지 vs 컨테이너 (빌드/실행/변경 관점)

| 구분 | 이미지 (Image) | 컨테이너 (Container) |
|------|----------------|----------------------|
| 개념 | 실행을 위한 템플릿 (설계도) | 이미지 기반으로 생성된 인스턴스 |
| 생성 방식 | `docker build`, `docker pull` | `docker run` |
| 빌드 | Dockerfile통해 빌드되거나 외부에서 pull | 이미지를 기반으로 생성됨 (빌드 개념 없음) |
| 실행 | 실행 불가 (정적 상태) | 실행 가능 (동적 상태) |
| 변경 가능 여부 | ❌ 불변 | ⭕ 변경 가능 (파일 수정, 상태 변화) |
| 재사용성 | 여러 컨테이너에서 공유 | 개별 컨테이너마다 독립 |
| 삭제 시 영향 | 삭제해도 기존 컨테이너 유지 가능 | 삭제하면 실행 상태 사라짐 |
- `Dockerfile` -> `build`: 이미지생성 -> `Image` -> `run`: 컨테이너 생성 -> `Container`

## 3. Dockerfile 기반 커스텀 이미지 제작


## 4. 포트 매핑


## 5. 바인드 마운트 및 볼륨 영속성


## 6. Git 설정 및 연동


## 7. Docker Compose


## 8. 트러블 슈팅

### [1] 히스토리 확장(History Expansion)으로 오인
| 구분 | 내용 |
|------|------|
| **문제** | `echo "hello codyssey!" > hello.txt` 입력 시 `dquote>` 가 나타나며 명령이 실행되지 않음 |
| **원인** | `!"` 에서 `!` 와 `"` 가 붙어있어 쉘이 닫는 따옴표를 제대로 인식하지 못함 |
| **해결** | 큰따옴표 `"` 대신 작은따옴표 `'` 사용: `echo 'hello codyssey!' > hello.txt` |