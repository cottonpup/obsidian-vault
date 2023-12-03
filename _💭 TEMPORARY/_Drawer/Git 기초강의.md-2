[깃 브랜치 배우기](https://learngitbranching.js.org/?locale=ko)
Dd

# 깃이란?
Git 은 오픈소스이며 무료 소스 관리 시스템이다

# 깃 다운로드하기
https://git-scm.com/downloads
https://code.visualstudio.com/
깃을 다운 받을 때, `Git bash`라는 터미널과 함께 같이 설치된다.
Window `PowerShell` 도 사용가능

# 깃 설정하기
## 깃 기본설정
`git config --global user.name "{변경할 이름}"`
`git config --global user.email {email}`

## 깃 브랜치 디폴트 이름설정
`git config --global init.default branch main`

# 리포지토리 초기화하기 
`cd` 커맨드로 해당 리포지토리로 가서 `git init`

### .git 폴더
Show Hidden items
![[Screenshot 2023-07-19 at 8.10.46 PM.png]]

### git 상태 확인
`git status` 

# git 의 세가지 영역

![[Pasted image 20230719204204.png]]
# 깃 파일 추적하기
## Track
`git add {file name}`
or 
`git add .` `git add -A`
## Untrack
`git rm --cached {file name}`

# 깃 커밋
## 커밋하기
깃 커밋이란 이전 커밋 상태부터 현재 상태까지 변경 이력이 기록된 커밋
`git commit -m "{commit message}"`

`git commit -a -m "{commit message}"`

## 깃 차이점 확인하기
`git diff`

## 커밋 히스토리 확인하기
`git log`
`git log --oneline`

# 깃 커밋 메시지 컨벤션
https://meetup.nhncloud.com/posts/106
https://github.com/naver

feat: Add a camera feature
fix: 채팅 버그 수정

![[Screenshot 2023-07-19 at 9.57.41 PM.png]]

# 깃 브랜치
## 브랜치 생성
`git branch {branch name}`
## 생성된 브랜치들 확인
`git branch`
## 브랜치 변경
브랜치를 변경하기 전에는 무조건 변경된 사항을 먼저 커밋하기!
`git switch {branch name}`
`git branch -M main`

브랜치 생성하면서 변경
`git switch -c {branch name}`
## 브랜치 머지
`git merge -m "{merge message}" {branch name you want to merge with}`
## 브랜치 삭제하기
git branch -d {branch name you want to delete}

## 머지 충돌해결하기
HEAD => the current

# 깃허브
브랜치까지 푸쉬
`git push --all`

## git issues
## git pull requests
## git pull (git fetch + merge)
