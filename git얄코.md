git얄코

VCS: version  control system
추적하지 않는(untracked) 파일: Git의 관리에 들어간 적 없는 파일

Reset : 시간을과거로 해당과거로 돌아간후 이후 행적은 삭제
Revert : 이후 행적 삭제하는게아니라 이떄의 변화를 거꾸로 수행하는 캡슐을 하나추가 결과적으로 이전으로 돌아가는상태 (기록으로 남길 필요가있을때)
내역들을 유지하되 어느한부분에서 실행했던 내용만 취소해야 하는 경우

 reset 사용해서 과거로 돌아가기
git reset --hard (돌아갈 커밋 해시)
git reset --hard    (뒤에 커밋 해시가 없으면 마지막 커밋을 가리킴)

  revert 로 과거의 커밋 되돌리기
git revert (되돌릴 커밋 해시)  :wq로 커밋 메시지 저장
커밋해버리지 않고 revert하기
git revert --no-commit (되돌릴  커밋 해시)

1. 브랜치 생성 / 이동 / 삭제하기
add-coach란 이름의 브랜치 생성
git branch add-coach
브랜치 목록확인
git branch
브랜치로 이동
git switch add-coach
 브랜치 생성과 동시에 이동하기  기존의 git checkout -b (새 브랜치명)
git switch -c new-teams
🗑 브랜치 삭제하기
git branch -d (삭제할 브랜치명)
지워질 브랜치에만 있는 내용의 커밋이 있을 경우
즉 다른 브랜치로 가져오지 않은 내용이 있는 브랜치를 지울 때는
-d 대신 -D(대문자)로 강제 삭제해야 합니다.
git branch -D (강제삭제할 브랜치명)
브랜치 이름바꾸기
git branch -m (기존 브랜치명) (새 브랜치명)

3. 결과 살펴보기
git log: 위치한 브랜치에서의 내역만 볼 수 있음
여러 브랜치의 내역 편리하게 보기
git log --all --decorate --oneline --graph

3-3 브랜치 합치기
서로 다른 브랜치를 합치는 두 방식
merge : 두 브랜치를 한 커밋에 이어붙입니다.
브랜치 사용내역을 남길 필요가 있을 때 적합한 방식입니다.
다른 형태의 merge에 대해서도 이후 다루게 될 것입니다.

rebase : 브랜치를 다른 브랜치에 이어붙입니다.
한 줄로 깔끔히 정리된 내역을 유지하기 원할 때 적합합니다.
이미 팀원과 공유된 커밋들에 대해서는 사용하지 않는 것이 좋습니다.

merge는 reset으로 되돌리기 가능
merge도 하나의 커밋
merge하기 전 해당 브랜치의 마지막 시점으로

병합된 브랜치는 삭제
삭제 전 소스트리에서 add-coach 위치 확인
git branch -d add-coach

2. rebase로 합치기
new-teams 브랜치를 main 브랜치로 rebase
new-teams 브랜치로 이동!!!!!!!!!!!!!!!!
🛑 merge때와는 반대!
아래의 명령어로 병합
git rebase main
소스트리에서 상태 확인
main 브랜치는 뒤쳐져 있는 상황
main 브랜치로 이동 후 아래 명령어로 new-teams의 시점으로 fast-forward
git merge new-teams
new-teams 브랜치 삭제

3-4
브랜치 간 충돌
파일의 같은 위치에 다른 내용이 입력된 상황

당장 충돌 해결이 어려울 경우 아래 명령어로 merge 중단
git merge --abort
해결 가능 시 충돌 부분을 수정한 뒤 git add ., git commit으로 병합 완료

--------------github
GitHub 레포지토리 생성 후 복붙 명령어
git remote add origin (원격 저장소 주소) 
로컬의 Git 저장소에 원격 저장소로의 연결 추가
원격 저장소 이름에 흔히 origin 사용. 다른 것으로 수정 가능

git branch -M main
GitHub 권장 - 기본 브랜치명을 main으로

git push -u origin main 
로컬 저장소의 커밋 내역들 원격으로 push(업로드)
-u 또는 --set-upstream : 현재 브랜치와 명시된 원격 브랜치 기본 연결

원격 목록 보기
git remote
원격 지우기 (로컬 프로젝트와의 연결만 없애는 것. GitHub의 레포지토리는 지워지지 않음)
git remote remove (origin 등 원격 이름)

1. 원격으로 커밋 밀어올리기(push)
git push
이미 git push -u origin main으로 대상 원격 브랜치가 지정되었기 때문에 가능

2. 원격의 커밋 당겨오기(pull)
git pull

3. pull 할 것이 있을 때 push를 하면?
원격에 먼저 적용된 새 버전이 있으므로 적용 불가
pull 해서 원격의 버전을 받아온 다음 push 가능

push 할 것이 있을 시 pull 하는 두 가지 방법

git pull --no-rebase - merge 방식
소스트리에서 확인해보기
reset으로 되돌린 다음 아래 방식도 해보기

git pull --rebase - rebase 방식
pull 상의 rebase는 다름 (협업시 사용 OK)

1. 원격 추가하기
GitHub에 새 레포지토리 만들고 origin2로 추가


lesson5원격의 브랜치 다루기

1. 로컬에서 브랜치 만들어 원격에 push 해보기
from-local 브랜치 만들기
2.아래 명령어로 원격에 push
git push 
아래 명령어로 원격의 브랜치 명시 및 기본설정
git push -u origin from-local
3.브랜치 목록 살펴보기
GitHub에서 목록 보기
아래 명령어로 로컬과 원격의 브랜치들 확인
git branch --all

2. 원격의 브랜치 로컬에 받아오기
1.GitHub에서 from-remote 브랜치 만들기
git branch -a에서 현재는 보이지 않음
2.아래 명령어로 원격의 변경사항 확인
git fetch
git branch -a로 확인
3.아래 명령어로 로컬에 같은 이름의 브랜치를 생성하여 연결하고 switch
git switch -t origin/from-remote

3.원격의 브랜치 삭제
git push (원격 이름) --delete (원격의 브랜치명)

------------------유료파트
섹션5 git보다깊이알기
git의 3가지 공간

수정사항 화살표
commit되어 레포지토리에 들어간 후 수정사항이 발생하면 tracked 파일로써 스테이징을 기다리게 됩니다.

Working directory
untracked: Add된 적 없는 파일, ignore 된 파일
tracked: Add된 적 있고 변경내역이 있는 파일
git add 명령어로 Staging area로 이동

Staging area
커밋을 위한 준비 단계
예시: 작업을 위해 선택된 파일들
git commit 명령어로 repository로 이동

Repository
.git directory라고도 불림
커밋된 상태

파일의 삭제와 이동
git rm
tigers.yaml를 삭제해본 뒤 git status로 살펴보기

파일의 삭제가 working directory에 있음
git reset --hard로 복원

git rm tigers.yaml로 삭제하고 git status로 살펴보기

파일의 삭제가 Staging area에 있음
git reset --hard로 복원

git mv
tigers.yaml를 zzamtigers.yaml로 이름변경 뒤 git status로 살펴보기
복원 후 git mv tigers.yaml zzamtigers.yaml로 실행 뒤 비교

파일을 staging area에서 working directory로
git restore --staged (파일명)
--staged를 뺴면 working directory에서도 제거
예전) git reset HEAD (파일명)

reset의 세 가지 옵션
--soft: repository에서 staging area로 이동
--mixed (default): repository에서 working directory로 이동
--hard: 수정사항 완전히 삭제

--------------lesson 3.HEAD
Git의 HEAD
현재 속한 브랜치의 가장 최신 커밋

switch로 브랜치 이동해보기

main과 delta-branch

checkout으로 앞뒤 이동해보기
git checkout HEAD^
^ 또는 ~: 갯수만큼 이전으로 이동 EX) git checkout HEAD^^^, git checkout HEAD~5
⭐️ 커밋 해시를 사용해서도 이동 가능

git checkout (커밋해시)
git checkout - : (이동을) 한 단계 되돌리기

HEAD사용하여 reset하기
git reset HEAD(원하는단계) (옵션)
-------------lesson 4. fetch vs pull
fetch와 pull의 차이
fetch: 원격 저장소의 최신 커밋을 로컬로 가져오기만 함
pull: 원격 저장소의 최신 커밋을 로컬로 가져와 merge 또는 rebase

fetch한 내역 적용 전 살펴보기
원격의 main 브랜치에 커밋 추가
* git checkout origin/main으로 확인해보기

원격의 변경사항 fetch
* git checkout origin/main으로 확인해보기
* pull로 적용

원격의 새 브랜치 확인
git checkout origin/(브랜치명)
git switch -t origin/(브랜치명)
-------------section6 git보다 잘활용하기
기본적인 명령어들과 설명
git help
git의 모든 명령어들
git help -a

------------section7 프로답게 커밋관리
1.아래 명령어로 hunk별 스테이징 진행
git add -p
y또는n으로 각 헝크 선택
2. 변경사항을 확인하고 커밋하기
git commit -v
git diff --staged와 비교

lesson3 커밋하기 애매한 변화 치워두기
git stash    git stash save와 같음
3. 원하는 시점, 브랜치에서 다시 적용
git stash pop
4. 원하는 것만 stash 해보기
git stash -p
5. 메시지와 함께 스태시
git stash -m 'Add Stash3'
6. 스태시 목록 보기
git stash list

Stash 사용법 정리
명령어	설명	비고
git stash	현 작업들 치워두기	끝에 save 생략
git stash apply	치워둔 마지막 항목(번호 없을 시) 적용	끝에 번호로 항목 지정 가능
git stash drop	치워둔 마지막 항목(번호 없을 시) 삭제	끝에 번호로 항목 지정 가능
git stash pop	치워둔 마지막 항목(번호 없을 시) 적용 및 삭제	apply + drop
💡 git stash branch (브랜치명)	새 브랜치를 생성하여 pop	충돌사항이 있는 상황 등에 유용
git stash clear	치워둔 모든 항목들 비우기	

lesson4 커밋수정
마지막 커밋 수정
git commit --amend

커밋 메시지 한 줄로 변경
git commit --amend -m 'Add members to Panthers and Pumas'

lesson5 과거의 커밋들을 수정,삭제,병합,분힐
git rebase -i (대상 바로 이전 커밋)
명령어	설명
p, pick	커밋 그대로 두기
r, reword	커밋 메시지 변경
e, edit	수정을 위해 정지
d, drop	커밋 삭제
s, squash	이전 커밋에 합치기

section8 취소와 되돌리기 깊이알기
git clean
Git에서 추적하지 않는 파일들 삭제

lesson2 커밋하지않은 변경사항 되돌리기
git restore  특정 파일을 지정된 상태로 복구
워킹 디렉토리의 특정 파일 복구
파일명 자리에 . : 모든 파일 복구

변경상태를 스테이지에서 워킹 디렉토리로 돌려놓기
git restore --staged (파일명)
파일을 특정 커밋의 상태로 되돌리기
git restore --source=(헤드 또는 커밋 해시) 파일명

lesson3 reset햇어도 희망!
reflog 명령어
git reflog
reflog는 프로젝트가 위치한 커밋이 바뀔 때마다 기록되는 내역을 보여주고
이를 사용하여 reset하기 이전 시점으로 프로젝트를 복구할 수 있습니다.

section9 태그
lesson1 커밋에 태그달기
Git의 Tag
특정 시점을 키워드로 저장하고 싶을 때
커밋에 버전 정보를 붙이고자 할 때
마지막 커밋에 태그 달기 (lightweight)
git tag v2.0.0
현존하는 태그 확인
git tag
원하는 태그의 내용 확인
git show v2.0.0
태그 삭제
git tag -d v2.0.0
마지막 커밋에 태그 달기 (annotated)
git tag -a v2.0.0
입력 후 메시지 작성 또는
git tag v2.0.0 -m '자진모리 버전'
원하는 커밋에 태그 달기
git tag (태그명) (커밋 해시) -m (메시지)
원하는 버전으로 체크아웃
git checkout v1.2.1

lesson2 원격의 태그와 릴리즈
특정 태그 원격에 올리기
git push (원격명) (태그명)
특정 태그 원격에서 삭제
git push --delete (원격명) (태그명)
로컬의 모든 태그 원격에 올리기
git push --tags

section10 branch보다 깊이알기
다른 브랜치의 원하는 커밋 가져오기
cherry-pick 명령어 사용
Cherry 커밋 main 브랜치로 가져오기
main 브랜치에서 실행
git cherry-pick (체리의 해시)
fruit 브랜치의 Cherry와는 별개의 커밋

다른 가지의 잔가지만가져오기--
다른 브랜치에서 파생된 브랜치 옮겨붙이기
rebase --onto 옵션 사용
fruit 브랜치에서 파생된 citrus 브랜치를 main 브랜치로 옮겨붙이기
git rebase --onto (도착 브랜치) (출발 브랜치) (이동할 브랜치)
git rebase --onto main fruit citrus
citrus로 fast forward

다른 커밋들을 하나로 묶어 가져오기--
merge --squash 옵션 사용
git merge --squash (대상 브랜치)
변경사항들 스테이지 되어 있음
git commit 후 메시지 입력

협업을위한 브랜치활용법--
Gitflow
협업을 위한 브랜칭 전략
사용되는 브랜치들
브랜치	용도
main	제품 출시/배포
develop	다음 출시/배포를 위한 개발 진행
release	출시/배포 전 테스트 진행(QA)
feature	기능 개발
hotfix	긴급한 버그 수정

section11 분석하고 디버깅하기
log 더자세히알아보기 ---
옵션들을 활용한 다양한 사용법
각 커밋마다의 변경사항 함께 보기
git log -p
최근 n개 커밋만 보기
git log -(갯수)
통계와 함께 보기
git log --stat
더 간략히: --shortstat
한 줄로 보기
git log --oneline
--pretty=oneline --abbrev-commit의 줄임
변경사항 내 단어 검색
git log -S (검색어)
커밋 메시지로 검색
git log --grep (검색어)
자주 사용되는 그래프 로그 보기
--all : 모든 브랜치 보기
--graph : 그래프 표현
--decorate : 브랜치, 태그 등 모든 레퍼런스 표시
--decorate=no
--decorate=short : 기본
--decorate=full

차이살펴보기 diff--
git diff
워킹 디렉토리의 변경사항 확인
git diff
파일명만 확인
git diff --name-only
스테이지의 확인
git diff --staged
--cached와 같음
커밋간의 차이 확인
git diff (커밋1) (커밋2)
커밋 해시 또는 HEAD 번호로
현재 커밋과 비교하려면 이전 커밋만 명시

브랜치간의 차이 확인
git diff (브랜치1) (브랜치2)

누가 코딩햇는지 알아내기--
git blame
각 라인의 작성자를 확인합니다.
파일의 부분별로 작성자 확인하기
git blame (파일명)
특정 부분 지정해서 작성자 확인하기
git blame -L (시작줄) (끝줄, 또는 +줄수) (파일명)

오류발생 시점 찾아내기
git bisect
이진 탐색 알고리즘으로 문제의 발생 시점을 찾아냅니다.
 v3 시점이 의심되는 상황
이진 탐색 시작
git bisect start
오류발생 지점임을 표시
git bisect bad
의심 지점으로 이동
git checkout (해당 커밋 해시)
오류 발생 않을 시 양호함 표시
git bisect good
♻️ 원인을 찾을 때까지 반복
git bisect good/bad
이진 탐색 종료
git bisect reset

section12 git의 추가기능들
git hooks
Git상의 이벤트마다 자동으로 실행될 스크립트를 지정합니다.
Git Hooks 폴더 보기
프로젝트 폴더 내 .git > hooks 폴더 확인
파일 끝에 .sample을 없애면 훅 실행파일이 됨

git submodule---

section13 github 잘 사용하기
lesson 1 프로젝트와 폴더에 대한 문서
lesson 2 풀리퀘스트와 이슈
1. Pull request
변경사항을 merge하기 전 리뷰를 거치기 위함
팀원들의 동의를 거친 뒤 대상 브랜치에 적용

풀 리퀘스트 사용해보기
새로운 브랜치 생성 후 변경사항 커밋하여 푸시
GitHub 레포지토리 페이지에서 Compare & pull request 버튼 클릭
또는 ~ branches에서 New pull request 클릭
메시지 작성 후 Create pull request 클릭

풀 리퀘스트 검토 후 처리하기
GitHub 레포지토리 페이지에서 Pull requests 탭 클릭
대상 풀 리퀘스트 클릭하여 내용 검토

의견이 있을 시 코멘트 달기
반려해야 할 시 Close pull request
승인할 시 Merge pull request




















