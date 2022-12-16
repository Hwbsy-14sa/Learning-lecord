# [Mac] "oh-my-zsh : Can't update" & "xcrun error" 해결하기 (2022-12-13)

</br>

## 1. 문제발생

---

"iterm2"을 실행 하였을 때, 아래와 같은 문구를 볼 수 있었다. </br>

> <span style= "color: red"> [oh-my-zsh] Can't update: not a git repository.</span>

## 2. 현상분석

---

셸 스크립트 이상여부를 확인해보기 위해 **`omz version`** 을 확인해본 결과 version이 확인되지 않으며 아래와 같은 문구가 출력된다.

> `<detached> ()` </br>

1.  `OMZ 폴더`에 디렉터리가 없어서 `.git`이 삭제되었을 것 으로 추정된다.</br>

2.  `macOS Update`시 간혹 발생 할 수 있는 사항이라고 한다.

- 최근 <span style=color:orange>**`Ventura 13.0.1`**</span>로 Update를 진행했었다.

## 3. 문제해결

---

1. 우선 git 상태를 확인해보기 위해 **`git --version`** 출력해본 결과 아래문구를 볼 수 있었다.

> <span style="color:red"> xcrun: error: invalid active developer path (/Library/Developer/CommandLineTools), missing xcrun at: /Library/Developer/CommandLineTools/usr/bin/xcrun` </span>

2. x-code Command Line Tools Error 라고하며 아래와 같은 방법으로 해결하였다.

> <span style="color:orange">`xcode-select --install`</span>

**"도구를 지금 설치하시겠습니까?"** 문구가 나올 때 **"설치"**를 누르면 </br>
수분의 시간이 소요되고 설치가 완료되었다고 뜬다.

<img width="506" alt="install" src="https://user-images.githubusercontent.com/58798715/207377116-00ce3168-5997-41f8-aee4-dde7c9709443.png">

## 4. 결과확인

---

<span style="color:orange">**git** & **omz** version check </span> 정상으로 확인 된다.

<img width="1168" alt="스크린샷 2022-12-14 00 53 58" src="https://user-images.githubusercontent.com/58798715/207381358-07a1b27a-2a24-49b8-b96f-9d42d586cf3d.png">
