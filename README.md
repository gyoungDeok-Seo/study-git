# git(웹개발)

## 버전 관리 시스템
	원하는 시점(버전)으로 이동할 수 있으며, 각 버전별로 
	여러 개발자가 협업할 수 있는 최적의 환경을 제공하는 시스템

## SVN
	작업내역 커밋시 변경사항과 히스토리가 즉시 서버로 전송되기 때문에 관리가 용이하다.
	또한 간단한 설치와 사용방법으로 별도의 교육 없이도 초보자도 쉽게 사용할 수 있다.
	하지만 항상 원격 저장소(SVN 서버)를 필요로 하며 서버간 버전 관리가 힘들다.

## Git(분산형 버전 관리 시스템)
	SVN이 가지고 있던 클라이언트와 서버 간의 버전 관리 문제를 많이 보완해준 시스템.
	서버 뿐만 아니라 로컬에서도 버전 관리가 가능하며, 로컬이 서버가 될 수 있고, 서버도 로컬이 될 수 있다.
	브랜치라는 개념을 사용하여 개발자 마음대로 로컬환경에서도 커밋과 버전 관리가 가능하다.

## 저장소의 종류
- 로컬 저장소(local): 개인 전용
- 원격 저장소(remote): 공유 전용

## 작업 트리(Work-Tree)
	폴더 또는 디렉터리를 의미한다.

## 스테이징 - add
	작업 트리를 커밋하기 전, 파일 상태를 기록하는 임시 공간.
	커밋하기 전 반드시 인덱스에 추가해야 하며, 이를 스테이징이라고 한다.
	변경한 모든 파일을 커밋하지 않고, 원하는 파일만 골라서 스테이징을 하게 되면
	인덱스에 등록된 파일들만 커밋된다. 인덱스에 등록되지 않은 파일들은 커밋이 될 수 없다.

## 커밋 - commit
	버전을 만들 때 사용한다.
	예를 들어 A와 B라는 파일이 있다면, 이를 하나의 버전으로 관리하고자 할 때 커밋을 사용한다.
	커밋 시 고유한 커밋 아이디가 부여되며, 원하는 버전으로 돌아갈 때 커밋 아이디 중 앞 7글자를 사용한다.

## 체크아웃 - checkout
	원하는 버전 또는 브랜치로 이동하고 싶을 때 사용한다.
	체크아웃 명령어 뒤에 커밋 아이디 전체 또는 앞 7글자를 작성하면 해당 버전으로 이동하게 된다.


## 브랜치 - branch
	한 개의 처리 경로를 여러 개의 처리 경로로 나눌 때 사용한다.
	보통 동시에 버전 관리를 해야 할 때 사용하며,
	기본 브랜치는 master이다.
   
   1. 커밋3 상태에서 hds 브랜치 생성
   
                        [master]
                        ↓
            커밋1----커밋2-----커밋3
                        ↑
                        [hds]
              

   2. hds 브랜치에서 커밋4 진행
   
                        [master]
                        ↓
            커밋1----커밋2-----커밋3----커밋4
                                  ↑
                                  [hds]
                     
   3. master 브랜치에서 커밋5 진행
   
                                    [master]
                                    ↓
                            ┌------커밋5
            커밋1----커밋2-----커밋3
                            └------커밋4
                                    ↑
                                    [hds]   
                        
   4. [HEAD] 포인터의 역할

            브랜치 혹은 커밋을 가리키는 포인터이며, [HEAD]를 통해 현재 커밋 상태를 표시해준다.
            또한 최신 커밋이 아닌 과거 커밋으로도 이동할 수 있다.

                                    [master]
                                    ↓
                            ┌------커밋5
            커밋1----커밋2-----커밋3
                            └------커밋4
                                    ↑
                                    [hds]
                                    [HEAD]

## 순서
	git init
	git add .
	git status
	git commit -m "메시지"
	git log --pretty=oneline	- 로그 한줄로 출력
	git checkout [커밋아이디, 브랜치명]	- 작성한 커밋버전 또는 브랜치로 이동
	git branch [브랜치명]		- 브랜치 생성
	git checkout -b [브랜치명]		- 브랜치 생성 및 생성한 브랜치로 이동
	git merge [브랜치명]		- 현재 브랜치와 입력한 브랜치 멀지 실행
	git remote add [원격 저장소 이름] [서버의 경로]
	git remote -v
	git remote remove [원격 저장소 이름]
	git push [원격 저장소 이름] [원격 저장소의 브랜치]

    팀장
        organization 생성
    팀원 초대
        repository 생성
    팀원 초대
        init(.gitignore)
        organization에 push

    전원
        fork

    팀원
        clone		- git clone 주소 .
        작업 브랜치 생성		- git checkout -b 브랜치명
        작업 진행		
        add			- git add .
        commit		- git commit -m "메시지"
        master 브랜치로 이동	- git checkout master
        병합			- git merge 브랜치명
        경로 확인		- git remote -v
        경로 변경		- git remote set-url origin https://github.com/본인닉네님/project.git
        push origin		- git push origin master
        PR
        팀장에게 연락
        작업 브랜치 이동
        작업 진행

    팀장
        팀원에게 연락 옴
        PR 확인
        충돌 시 선택 후 확정
        충돌 없을 시 Merge
        팀원 전체에게 연락: 전체 pull 받으세요

    팀원
        master 브랜치 이동
        경로 확인			- git remote -v
        경로 변경	- git remote set-url origin https://github.com/organization이름/project.git
        pull project			- git pull project(organization의 repository명) master
        작업 브랜치 이동
        다른 작업자의 코드가 필요하면 merge
        작업 진행
