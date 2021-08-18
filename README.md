# Git을 활용한 버전관리
1. [intall git & github](#intall-git--github)
1. [스타벅스 예제 GitHub 업로드](#스타벅스-예제-github-업로드)
1. [Netlify 지속적인 배포](#netlify-지속적인-배포)
1. [수정사항 버전 생성](#수정사항-버전-생성)
1. [로그인 브랜치](#로그인-브랜치)
1. [로그인 브랜치 병합](#로그인-브랜치-병합)
1. [프로젝트 복제](#프로젝트-복제)
1. [연습-버전 되돌리기](#연습-버전-되돌리기)
1. [연습-다른 환경에서 시작하기](#연습-다른-환경에서-시작하기)
1. [연습-충돌, 로컬 병합](#연습-충돌-로컬-병합)

# Git을 활용한 버전관리
## intall git & github
[git](https://git-scm.com/) 설치
```bash
$ git --version
```

[github](https://github.com/) 계정 생성
## 스타벅스 예제 GitHub 업로드
[github](https://github.com/) repository 생성  
github에 push 할 떄 vscode 인증 허가  
`./starbucks/`
```bash
$ git init
$ git config --global core.autocrlf true
$ git config --global user.name 'alfer91'
$ git config --global user.email 'dasungwkd@naver.com'
$ git config --global --list
$ git status
$ git add .
$ git commit -m 'Start project'
$ git log
$ git remote add origin https://github.com/alfer91/starbucks.git
$ git remote -v
$ git push origin master
```

## Netlify 지속적인 배포
### 계정 생성 & 권한 허가
1. [netlify](https://www.netlify.com/) gihub으로 가입  
1. New site from Git - Github 선택
1. permission - Authorize Netlify 선택
    - All repositories
    - Only select repositories
1. install 선택
---
### 사이트 생성 from Git
1. New site from Git
    1. Connect to Git provider - Github 선택
    1. Pick a repository - alfer91/starbucks 선택
    1. Build options, and deploy! - Deploy site 선택 
---    
[https://eloquent-villani-c6bc14.netlify.app](https://eloquent-villani-c6bc14.netlify.app)

## 수정사항 버전 생성
```bash
$ git add .
$ git commit -m '뱃지 이미지 수정'
$ git add .
$ git commit -m 'README.md 추가'
$ git push origin master
```
[netlify](https://www.netlify.com/) 로그인 - Deploys - github의 commit 내역 자동 배포(continuos deploy) 

## 로그인 브랜치
```bash
$ git branch
$ git branch -a
$ git branch signin
$ git checkout signin
$ git add .
$ git commit -m '로그인 페이지 시작하기'
$ git add .
$ git commit -m '공통 모듈 분리'
$ git checkout master
```

## 로그인 브랜치 병합
```bash
$ git checkout sigin
$ git add .
$ git status
$ git commit -m '로그인 페이지 완성'
$ git push origin signin
```
[netlify](https://www.netlify.com/) 접속 - Site settings - build & deploy - continuos Deployment - Production branch: master 확인
___
### Branch Merge
1. sigin branch push
1. [github](https://github.com/) 접속
1. starbucks repository 이동
1. Pull requests 선택
1. New pull request 선택
1. base: master, compare: signin 변경
1. Create pull request * 2 선택
1. Merge pull request 선택
1. Confirm merge 선택

## 프로젝트 복제
```bash
$ dir
$ cd .\Desktop\
$ git clone https://github.com/alfer91/starbucks.git
$ cd .\starbucks\
$ code . -r
```

## 연습-버전 되돌리기
`./git-practice/` from mac
```bash
$ git init
$ git add .
$ git commit -m "1"
$ git add .
$ git commit -m "2"
$ git add .
$ git commit -m "3"
$ git reset --hard HEAD~1
$ git reset --hard ORIG_HEAD
$ git reset --hard HEAD~2
$ git reset --hard ORIG_HEAD
$ git branch purple
$ git branch
$ git checkout purple
$ git add .
$ git commit -m 'purple/1'
$ git checkout master
$ git add .
$ git commit -m '4'
$ git remote add origin https://github.com/alfer91/git-practice.git
$ git push origin masater
$ git checkout purple
$ git push origin purple
```

## 연습-다른 환경에서 시작하기
`vscode terminal` from window
```bash
$ dir
$ cd .\Desktop\
$ git clone https://github.com/alfer91/git-practice.git
$ cd .\git-practice\
$ code . -r
$ git branch
$ git branch -r
$ git checkout -t origin/purple
$ git checkout master
$ git branch -d purple
$ git checkout -b yellow
$ git push origin yellow
```

## 연습-충돌, 로컬 병합
1. window, mac - master: `4` commit에서 시작  
1. window에서 먼저 `XYZ` commit push
1. 뒤이어 mac에서 `ABC` commit push & rejected 
    1. commit 한 단계 `reset` 후 pull `XYZ` commit 
    1. pull `XYZ` commit & `merge`
1. mac에서 `ABYZ` commit & push
1. window에서 pull `ABYZ`  

from window
```bash
$ checkout master
$ git add .
$ git commit -m 'XYZ'
$ git push origin master


$ git pull origin master // `ABYZ`
```
from mac
```bash
$ checkout master
$ git add .
$ git commit -m 'ABC'
$ git push origin master // rejected


$ git pull origin master // conflict
$ git add .
$ git commit -m 'ABYZ'
$ git push origin master
```
or
```bash
$ git reset --hard HEAD~1
$ git pull origin master 
```

