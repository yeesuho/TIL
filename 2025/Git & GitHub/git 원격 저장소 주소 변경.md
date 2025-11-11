2025.11.11

귀찮아서 오랫동안 안쓰다가 다시 TIL을 써보려고 합니다 <br>
얼마나 꾸준히 할지는 몰라요..ㅎ 그냥 일기장처럼 쓰고싶을 때 쓰겠습니다

# git 원격 저장소 주소 변경
찾아보니까 remote를 변경할때 굳이 remote를 삭제했다가 다시 연결하지 않아도 되더라고요

먼저 git remote가 연결되어있는지 확인하기 위해서는 아래와 같이 `git remote -v` 명령어를 입력해 확인할 수

```git
git remote -v

# origin  https://github.com/user/repo.git (fetch)
# origin  https://github.com/user/repo.git (push)
```

확인 후 git remote set-url origin <변경할 원격 저장소 주소> 를 입력하면 원격 저장소 주소가 변경됩니다

```git
git remote set-url origin https://github.com/user/변경할repo.git
```

