git정리
##초보자를 위한 간단한 Git 튜토리얼
-https://nulab.com/ko/learn/software-development/git-tutorial/
##Most useful git commands: 
-https://orga.cat/posts/most-useful-git-commands

git add/commit할때
ls -a 해서 .git보이는폴더에서 명령어입력

echo "# -" >> README.md
git init
git add README.md
git commit -m "first commit"
git branch -M main
git remote add origin (레포짓주소)
git push -u origin main

1. staging area는 commit을 하기 전에 commit할 파일들을 골라놓는 곳입니다.
그리고 staging area에 파일넣는 행위를 staging이라고 합니다. 
git add 명령어로 staging 할 수 있습니다.

2. repository는 commit된 파일의 버전들을 모아놓는 곳입니다.
repository의 실체를 구경하고 싶으면 작업폴더안에 숨겨져 있는 .git 폴더 열어보면 됩니다. 

아무튼 staging area & repository 2개는 자주 쓰는 용어니까 잘 외워둡시다.

-------------------------git add,commit
git add 파일명1 파일명2
이렇게 여러 파일을 동시에 스테이징할 수 있습니다.
git add .
작업폴더의 모든 파일을 전부 스테이징하고 싶으면 git add . 하면 됩니다.
 
git add 파일명 
git commit -m '아무메세지'

git restore --staged 파일명
스테이징된 파일을 취소하고 싶으면 하면 이거 입력하면 됩니다.
터미널에서 자주 알려주는 명령어라 외울 필요는 없습니다.

저기서 파일명 대신 점찍으면 어떻게 될까요

git commit -m '메세지'
commit 할 때 -m 뒤에 메세지 입력가능합니다. 

git log --all --oneline
git log --all --oneline --graph
commit 기록을 한 눈에 파악하고 싶으면 git log 명령어 입력하면 됩니다. 
--graph 옵션을 넣으면 그래프로 그려줍니다. 지금은 보잘것 없음 
다만 입력 후엔 Vim 에디터가 켜져서 j, k 키로 위아래 스크롤이 가능하고 q 키로 종료할 수 있습니다. 

-------------git의 branch
브랜치 생성은 git branch 브랜치명
브랜치 이동은 git switch 브랜치명 
브랜치 합치기는 main/master 브랜치로 이동한 뒤에 git merge 브랜치명
브랜치마다 commit 내역을 그래프로 보고싶으면 git log --graph --oneline --all
브랜치 합칠 때 conflict가 발생하면 파일열어서 수정하고 git add, git commit 하기 

------------git의 merge
**case1 각 브랜치에 신규commit이 있는경우 -3way merge  제일일반적
**case2 기준 브랜치에 신규commit이 없는경우 --새 브랜치를main브랜치로 지정
 -fast forwardmerge
merge 완료된 브랜치 삭제는 git branch -d 브랜치명
merge 안한 브랜치 삭제는 git branch -D 브랜치명
**case3  rebase한후 fastfoward 
rebase이유: 간단하고 짧은 브랜치들은이게 깔끔 git log 깔끔
단점: conflict 많이 발생
ex)
일반적 merge 하고싶으면 
1.중심브랜치로 이동해서 2.git merge 새로운브랜치명
rebase&merge 하고싶으면
1.새로운브랜치로 이동해서 2.git rebase 중심브랜치명
3.중심브랜치로 이동해서 4.git merge 새로운브랜치명
**case4. squash and merge
git merge --squash 새브랜치

---------git revert,reset,restore

파일 하나를 되돌리려면 git restore 
git restore 파일명
이러면 최근 commit 된 상태로 현재 파일의 수정내역을 되돌릴 수 있습니다. 
git restore --source 커밋아이디 파일명
이러면 입력한 파일이 특정 커밋아이디 시점으로 복구됩니다. 
git restore --staged 파일명
이건 복구랑 상관없지만 이러면 특정 파일을 staging 취소할 수 있습니다. 

commit을 되돌리려면 git revert 
git revert 커밋아이디
이거 입력하면 그 커밋아이디에서 일어난 일만 취소해줍니다. 
없애버리는건 아니고 commit 하나를 취소한 commit을 하나 생성해줍니다. 
commit1--commit2--commit3 에서
git revert commit2를하면
commit2--commit2--commit3--commit4(commit2내용 삭제됨)
그냥 최근 했던 commit 1개만 revert하고 싶으면 git revert HEAD 하면 편리

git reset 명령어 사용하면 특정 commit 시절로 아예 모든걸 되돌릴 수 있습니다. 
git reset --hard 커밋아이디
입력하면 그 커밋이 생성될 때로 시간을 되돌려줍니다.
commit1--commit2--commit3 에서
git reset --hard commit2
commit1--commit2

---------github1 내코드올릴땐 git push
.git이 repository(git이 파일 기록해두는 장소)
git init 는 repository생성 명령어

git branch -M main
입력하면 기본 브랜치 이름이 변경됩니다. 

Github에서 만든 원격 저장소에 올리기
로컬저장소 -> 원격저장소
이렇게 업로드하고 싶으면 작업폴더에서 터미널켜서
git push -u 원격저장소주소 main
-u 옵션은 방금 입력한 주소 기억해두라는 뜻입니다. 다음부터는 주소를 길게 입력안하고 git push만 입력해도 잘됩니다.
원격 repository 주소는 이렇게 https:// 부터 시작해서 .git으로 끝납니다.

git remote add origin https://github.com/codingapple1/lesson.git
이렇게 입력하면 "https://어쩌구" 주소가 필요할 때 마다 origin 이라는 변수명을 쓸 수 있습니다. 
아까쓰던 지랄맞게 길던 명령어를 git push -u origin main 이렇게 짧고 귀엽게 쓸 수 있겠군요. 

원격저장소에 있던거 그대로 내려받기
git clone https://원격저장소주소

-------------Github 사용법 2. 타인과 협업하기 (git clone, pull)

git clone 원격저장소주소

 원격 vs 로컬 내용이 다르다면 로컬저장소에서 git push가 안됩니다.
git pull 이용하면 현재 원격저장소 내용 가져올 수 있음 
git pull 원격저장소주소
러면 원격저장소에 있던 모든 브랜치 내용을 가져와서 로컬저장소에 합치라는 뜻입니다.

이걸 해주면 로컬이 원격저장소 내용을 반영한 최신상태가 되기 때문에 이제 git push가 가능합니다.
결론은 변동사항이 생겼다면 git pull 하고 나서 git push 하면 됩니다.
cf)
- git pull 원격저장소주소 브랜치명 입력하면 특정 브랜치만 가져올 수 있습니다. 
- origin이라는 변수명을 등록해놨으면 당연히 사용가능
- 예전에 -u 했었으면 git pull, git push까지만 입력해도 잘됩니다.
git pull 입력하면 자동으로 git fetch + git merge를 해줍니다. 

------------------Github 사용법 3. 브랜치로 협업하기 (pull request)
로컬 브랜치를 원격에 올리고 싶으면
git push 원격저장소주소 로컬브랜치명
git push 원격저장소주소 하면 모든 로컬저장소 브랜치 -> 원격저장소 입니다.






