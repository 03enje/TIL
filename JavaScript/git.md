## GIT Repository 포크

- 원하는 저장소를 가져올 때 사용하는 명령어입니다.

git clone (repository url) // 저장소 복사

cd (repository) // 저장소 경로 이동

git remote -v // 원격 저장소 확인

> git은 원격 저장소와 로컬 저장소가 있으며 원격 저장소는 github에 저장된 저장소를 의미하며 로컬 저장소는 사용자 컴퓨터에 저장된 저장소를 의미합니다.

### git upstream 저장소 추가

- 다른 사람의 저장소를 복사(fork)할 경우 자신의 계정에 저장된 저장소는 origin이 되며 복사한 계정에 있는 저장소는 upstream이 됩니다. 따라서 upstream 저장소의 파일이 변경될 때 마다 항상 가져올(fetch) 필요가 있으므로 다음과 같은 명령어로 가져올 수 있습니다.

git remote add upstream (repository ulr) // upstream 원격 저장소 추가

git remote -v // 원격 저장소 확인

git fetch upstream // upstream 저장소에서 파일 가져오기

git checkout main // 분기를 origin 저장소의 main 분기로 변경

git merge upstream/main // upstream 저장소의 main 분기에 있는 파일을 현재 origin 저장소와 병합(merge)

### git 분기(branch) 생성

- git 저장소에는 분기(branch)가 존재합니다. 분기란 간단하게 나무에서 자란 가지를 생각하면 됩니다. 하나의 나무에서 여러개의 가지가 펼쳐지듯이 git도 저장소가 여러개의 분기로 이루어져있습니다. 따라서 여러개의 분기로 나눠 파일을 관리하거나 하나로 합쳐서 관리할 수도 있습니다.

git branch (user branch) // git 분기 생성

git checkout (user branch) // 생성된 분기로 변경

### git 분기에 기여하기

git add . // git 분기의 스테이지에 변경된 파일을 추가

git commit -m ("message") // 파일을 추가하기 전 확인 메시지 작성

git push // 파일을 추가

### The current branch (user branch) has no upstream branch. To push the current branch and set the remote as upstream.

새로 생성된 분기는 자동적으로 upstream 저장소를 찾지(tracking) 못하기 때문에

git push --set-upstream origin (user branch)

와 같은 명령어를 입력해 git push를 해줘야 합니다. 하지만 항상 push할 때마다 시도한다면 번거롭기 때문에 다음과 같은 명령어를 입력해 자동적으로 push하게 해줍니다.

git config --global --add push.autoSetupRemote true // 해당 옵션은 앞으로 origin 저장소만든 새로운 분기에서 git push를 하면 자동적으로 upstream을 트래킹하여 추가하게 해줍니다.

### git commit 추가 기능

<git 커밋 합치기>

git rebase -i HEAD~3 :: 숫자는 HEAD에서 갯수

VI 창에서 a를 눌러 합칠 커밋을 HEAD는 pick 나머지는 s로 수정
wq!로 저장
HEAD 커밋 메시지만 원하는 메시지로 변경 wq!로 저장
git push -f

<git 로그>

git log :: 깃 로그 (나가기 Q)

<git 커밋 복구>

git reset --hard :: 깃 커밋 복구 (커밋 지점)

git push -f origin

<git 커밋 스테이지 삭제>

git restore staged 파일명 :: 스테이지 수정된 내용 삭제

### git 사용자 설정

<git ingnore>

https://www.toptal.com/developers/gitignore 해당 사항 gitignore에 추가

<git add . vs git add\*>

git add . :: gitignore에 기재된 것 고려하여 모두 추가

git add \* :: gitignore에 기재된 것 상관없이 모두 추가
