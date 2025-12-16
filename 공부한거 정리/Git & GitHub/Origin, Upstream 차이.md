2025.05.01


## origin
- 내가 클론한 원격 저장소

- 예를 들어 GitHub에서 어떤 프로젝트를 git clone 했다면 그 원격 저장소의 기본 이름은 origin

- 즉 내가 직접 작업을 올리는 곳

```bash
git remote -v
# origin  https://github.com/내아이디/레포.git (fetch)
# origin  https://github.com/내아이디/레포.git (push)
```


## upstream
- 원본 저장소 즉 내가 포크한 대상 저장소

- 다른 사람이나 조직이 만든 프로젝트를 포크해서 작업할 경우 <br>그 원본을 upstream이라는 이름으로 등록

```bash
git remote add upstream https://github.com/원저장소/레포.git
```

```bash
git remote -v
# origin    https://github.com/내아이디/레포.git (fetch)
# upstream  https://github.com/원저장소/레포.git (fetch)
```