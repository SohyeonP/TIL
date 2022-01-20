### **Git Repository 변경**
---

기존에 Git에 올라가 있는 프로젝트를 새로운 레포지토리로 이동시켜야 하는 작업을 해야했다.




우리가 잘 아는 `git clone` 을 사용 하면 그동안 `commit`이나 `Pull Reqeust` 기록들이 사라지기 때문에
다른 방밥인 `git mirror`를 사용해야 한다. 찾아보니 다양한 방법이 있었다.

### **Mirror Vs Bare**
--- 
**Mirror**: 

소스 저장소(repository) 의 mirror 를 설정한다. 이 옵션은 --bare 옵션을 포함한다. --bare 옵션과 비교해서 --mirror 는 원본의 지역 브랜치를 타겟의 지역 브랜치에 매핑할 뿐 아니라, 모든 refs (원격 브랜치, notes 를 포함하여)를 매핑한다. 그리고, 모든 refs 는 목표 저장소(복사되는 저장소 target repository) 에서 git remote update 를 실행함으로써 refspec 구성(configuration) 을 설정한다.

**Bare** : 로컬 저장소에 `Git Repository`를 bare로 만든다.자체 `$GIT_DIR`을 이용하기 때문에 기본적으로 -n 옵션을 사용 `working tree`에 체크아웃할 곳이 없음.

`bare clone`과 `non-bare-clone` 의 차이

* `bare clone` -> `branch` 직접복사
* `non-bare clone` -> `remote ref branch`설정, Head를 위한 `local branch` 생성


### **사용법**
---
* 공부의 용도로 기존의 ref가 필요하지 않음/독립적인 repository사용 -> clone(non-bare)
* 기존의 ref 필요 하지만 원격브랜치는 필요하지 않음(위의 내용포함) -> clone --bare
* 전체 정보  ref와 branch 가 모두 필요/기존 저장소와 같은환경이 만들어진다. 원본과 교체할수있음 -> clone -mirror

### **Repository 미러링 하기**

1. 옮길 repository를 clone bare 를 한다.

```
$ git clone --bare https://github.com/exampleuser/old-repository.git
```

2. clone 받은 경로로 진입후 새로운 repository에 push -mirror 진행
 
```
$ cd old-repository
$ git push --mirror https://github.com/exampleuser/new-repository.git
```

3. 1번에서 만든 임시 로컬 repository는 제거 한다.

```
$ cd ..
$ rm -rf old-repository
```
---

### **Repository 미러링 하기**(Git 대용량파일저장소 개체가 포함된 경우)

1. 옮길 repository를 clone bare 를 한다.

```
$ git clone --bare https://github.com/exampleuser/old-repository.git
```

2. clone 받은 경로로 진입
 
```
$ cd old-repository
```

3. repository의 Git 대용량 저장소 개체를 가져옴

```
$ 햣git lfs fetch --all
```

4. 위의 작업후에 push 작업을 진행& 대용량 저장소 개체도 push(**순서 유지**)

```
$ git push --mirror https://github.com/exampleuser/new-repository.git -- 1 
$ git lfs push --all https://github.com/exampleuser/new-repository.git -- 2
```
5. 이전에 만든 임시 repository 삭제
```
$ cd ..
$ rm -rf old-repository
```

밑의 그림은 위의 설명을 좀더 잘 알수 있게 도식화된 자료 


![gitmirror](/image/gitmirror.jfif)


**참조 문서**

[GithubDoc](https://docs.github.com/en/repositories/creating-and-managing-repositories/duplicating-a-repository)

[gitclone/bare차이](https://pinocc.tistory.com/138)

[StackoverFlow](https://stackoverflow.com/questions/3959924/whats-the-difference-between-git-clone-mirror-and-git-clone-bare)

[Tistroy](https://www.whatwant.com/entry/bare-%EC%99%80-mirror%EC%9D%98-%EC%B0%A8%EC%9D%B4)