# OSS3TEAM_6w_Chapter-6
6장 브랜치 요약입니다.
-----------------------------------------
<br/>

# 6-1. 새로운 작업
## 6-1-1. 브랜치 작업
### 📌 브랜치(branch)
나뭇가지, 지사, 분점 등 줄기 하나에서 뻗어 나온 갈림길을 의미함.

▶️  **저장 공간 하나에서 가상의 또 다른 저장 공간을 만드는 것!**

▶️  **개발자는 항상 안정된 코드 상태를 유지하고 개발 중인 작업과 구분하여 코드를 관리해야 하므로 이를 위해 사용하는 기능**

▶️  **잦은 버그 수정과 새로운 기능 구현 등을 위해 원본을 기반으로 새로운 사본에 기능을 추가하는 작업을 '브랜치 작업' 이라고 함.**
<br/><br/>

### 📌 git을 사용한 브랜치 작업의 이점
- 우리가 오랫동안 해 왔던 브랜치 작업의 과정  
  : 많은 내용 변경이 예상됨. --> 작업 폴더를 통째로 복사 --> 복사한 폴더 이름 변경 --> 기존의 코드는 남겨 두고, 복제된 작업 폴더에서 도전적인 작업 수행 (코드 분리)
  
  - 단점
  1. 프로젝트 유지, 관리 측면에서 효율성이 떨어진다.
  2. 많은 프로젝트 폴더를 복제하다 보면 향후 코드 통합에 어려움이 생길 수 있다.

 ❗  **git**을 사용하면 **프로젝트 작업 폴더를 복사하지 않고 기존 코드와 분리해서 사용하는 것이 가능** (더 편리함)  ❗
<br/><br/>

### 📌 commit과 branch의 기능적 차이
- **commit** : 파일의 **수정 이력 관리**에 사용

- **branch** : 프로젝트를 **독립적으로 관리**하는 데 사용 
<br/><br/></br>

## 6-1-2. 깃 브랜치 특징
### 📌 가상 폴더
깃의 브랜치는 작업 폴더를 실제로 복사하지 않고 **'가상 폴더'** 로 생성하기 때문에 외부적으로는 물리적인 파일 하나만 있는 것처럼 보인다.

- 장점 : 브랜치로 생성된 가상 폴더는 빠르게 공간 이동이 가능하므로 개발자는 쉽게 브랜치를 이동하면서 유연한 개발을 하는 것이 가능하다.
<br/><br/>

### 📌 독립적인 동작
브랜치를 이용하면 원본 폴더와 분리하여 독립적으로 개발 작업을 수행할 수 있어 **분리된 브랜치**에서 코드 **작업**한 후 **원본 코드에 병합**하는 명령만 수행하면 된다.

- 장점 : 규모가 큰 코드 수정이나 병합을 처리할 때 매우 유용하다.
<br/><br/>

### 📌 빠른 동작
깃은 **'Blob 개념'** 을 도입하여 내부를 구조화한다. Blob는 포인트와 유사한 객체로 깃은 브랜치를 변경할 때 포인터(HEAD 포인터)를 이동하여 빠르게 전환한다.  

- 장점 : 브랜치 명령을 사용하면 내부적으로 커밋을 하나 생성하여 브랜치로 할당하는데, 다른 VCS(버전 관리 시스템)들은 폴더의 파일 전체를 복사하는 반면 깃은 41바이트를 가지는          해시(SHA1) 파일 하나만 만들면 되어 파일 크기가 커도 깃이 브랜치를 생성하는 속도가 다른 VCS보다 더 빠르다.
<br/><br/></br>


# 6-2. 실습 준비(git)
## 6-2-1. 저장소 생성 및 초기화
❗  깃은 기본적으로 **main 브랜치** 하나를 가지고 있고 브랜치는 **HEAD 포인터**를 가지고 있다.  ❗

1. 브랜치 실습을 위한 환경을 구축해 본다.

```bash
YuBeenSo@DESKTOP-SKBKL14 MINGW64 /c/coding/coding/2022 OSS
$ cd git     # cd 명령어를 이용하여 내 컴퓨터에서의 오늘 실습 메인 폴더인 git으로 이동한다.


YuBeenSo@DESKTOP-SKBKL14 MINGW64 /c/coding/coding/2022 OSS/git
$ mkdir gitstudy06     # mkdir 명령어를 이용하여 git 폴더 하부에 저장소로 사용할 'gitstudy06'이라는 이름의 새 디렉토리를 생성한다.


YuBeenSo@DESKTOP-SKBKL14 MINGW64 /c/coding/coding/2022 OSS/git
$ cd gitstudy06     # cd 명령어를 이용해 gitstudy06 폴더로 현재 위치를 변경한다.


YuBeenSo@DESKTOP-SKBKL14 MINGW64 /c/coding/coding/2022 OSS/git/gitstudy06
$ git init     # init(초기화) 명령어를 통해 gitstudy06 저장소를 초기화시킨다.
Initialized empty Git repository in C:/coding/coding/2022 OSS/git/gitstudy06/.git/


YuBeenSo@DESKTOP-SKBKL14 MINGW64 /c/coding/coding/2022 OSS/git/gitstudy06 (main)     
# 초기화가 완료되면 위와 같이 현재 'main' 브랜치라는 것을 알려준다.     

```

**현재 브랜치**가 **main**이라는 것을 확인할 수 있고 **현재 브랜치의 작업 위치**도 확인할 수 있다.
<br/><br/><br/>


## 6-2-2. 기본 브랜치
❗  모든 커밋과 이력은 브랜치에 기록되므로 깃은 최소한 브랜치가 1개 이상 필요하므로 저장소를 처음 초기화하면 main(혹은 master) 브랜치 하나가 자동으로 생성이 된다.  ❗

2. 저장소 초기화 후 status 명령어를 실행해 본다.

```bash
YuBeenSo@DESKTOP-SKBKL14 MINGW64 /c/coding/coding/2022 OSS/git/gitstudy06 (main)
$ git status     # status(상태) 명령어를 입력하면 아래와 같이 gitstudy06에서는 현재 commit할 파일이 없다는 문구가 나온다.
On branch main     # 현재 브랜치 작업 위치(main)

No commits yet

nothing to commit (create/copy files and use "git add" to track)
```

git에서는 항상 현재 작업하는 브랜치 위치를 확인하는 것이 중요하다.

다음과 같이 branch 명령어를 통해서도 현재 브랜치 확인이 가능하다.

```bash
YuBeenSo@DESKTOP-SKBKL14 MINGW64 /c/coding/coding/2022 OSS/git/gitstudy06 (main)
$ git branch
*main
```

branch 명령어는 생성된 모든 브랜치를 출력하는데 앞 코드에서는 깃에서 기본적으로 선택되는 브랜치인 main이 출력되었다. 하지만 꼭 main 이름으로 사용할 필요는 없다.
<br/><br/><br/>


# 6-3. 브랜치 생성
## 6-3-1. 브랜치 생성
### 📌 브랜치가 나타내는 것
- 브랜치는 **공통된 커밋**을 가리키는 지점이다.
- 브랜치는 또 하나의 **개발 분기점** 이다.
- 브랜치는 커밋처럼 **SHA1 해시키**를 가리킨다. but 해시키를 기억하기 어렵기 때문에 특정 커밋을 가리키는 **별칭**을 만드는데 이렇게 만든 별칭이 **브랜치**이다.

![브랜치는 공통된 커밋을 가리키는 지점](https://gitbookdown.dallasdatascience.com/img/git_branch_merge.png)

*(이미지 출처 : https://gitbookdown.dallasdatascience.com/branching-git-branch.html)*

위 그림에서 왼쪽에서 2번째 커밋 부분이 공통된 커밋을 가리키는 지점이므로 브랜치라고 할 수 있다.
<br/><br/>

### 📌 브랜치 생성
- **사용자 브랜치** : 처음 생성되는 기본 main 브랜치 외의 브랜치는 사용자가 직접 branch 명령어를 입력하여 생성해야 한다. (사용자가 직접 정의하는 브랜치)

- 브랜치 생성 개수에는 제한이 없다. 따라서 필요한 만큼 여러 브랜치를 생성하고 각 브랜치를 구별하기 위해 이름을 지정해 주면 된다.  
<br/>

❗  **브랜치 이름 생성하는 방법**  ❗

```bash
$ git branch 브랜치이름 커밋 ID
```

▶️ 위와 같이 입력하면 현재 **HEAD 포인터 기준**으로 내가 작성한 이름의 **새로운 브랜치**를 생성한다. 뒤에 지정한 **커밋 ID** 인자 값을 지정하면 지정한 **커밋 ID** 기준      으로 브랜치를 생성할 수 있다.

▶️ **새 브랜치를 생성하면 포인터만 있는 브랜치가 생성**된다. 이렇게 새롭게 생성된 브랜치는 독립된 공간을 할당하여 기존 작업 영역에 영향을 주지 않는 새로운 가상 공간이      된다.
<br/><br/>

3. 저장소에 새로운 파일을 하나 생성한 후 저장하여 실습 환경을 만들어 보자.

```bash
YuBeenSo@DESKTOP-SKBKL14 MINGW64 /c/coding/coding/2022 OSS/git/gitstudy06 (main)
$ code branch.htm     # branch.htm이라는 이름의 파일을 VSCODE를 통해 편집할 수 있게 해 준다.
```

```html
<h1>브랜치 실습을 합니다.</h1>     <!-- branch.htm 에 작성할 코드 내용 -->
```

```bash
YuBeenSo@DESKTOP-SKBKL14 MINGW64 /c/coding/coding/2022 OSS/git/gitstudy06 (main)
$ git add branch.htm     # 추적 등록

YuBeenSo@DESKTOP-SKBKL14 MINGW64 /c/coding/coding/2022 OSS/git/gitstudy06 (main)
$ git commit -m "first"     # 커밋 메시지 작성
[main (root-commit) 9f802ee] first
 1 file changed, 1 insertion(+)      # 커밋이 하나 생성되었다.     
 create mode 100644 branch.htm
```

마지막 커밋 ID인 100644를 기준으로 브랜치를 생성, 추가해 본다.

```bash
YuBeenSo@DESKTOP-SKBKL14 MINGW64 /c/coding/coding/2022 OSS/git/gitstudy06 (main)
$ git branch footer     # footer라는 이름의 브랜치 생성

YuBeenSo@DESKTOP-SKBKL14 MINGW64 /c/coding/coding/2022 OSS/git/gitstudy06 (main)
$ git branch     # 브랜치 목록 확인
  footer     # 생성된 브랜치
* main     # 현재 브랜치
```
<br/><br/>

## 6-3-2. 브랜치 이름
### 📌 브랜치 이름 작성 규칙
- 기호(-), 마침표(.)로 시작이 불가하다.
- 연속적인 마침표(..)를 포함할 수 없다.
- 빈칸, 공백 문자, 물결(~), 캐럿(^), 물음표(?), 별표, 대괄호([]) 등은 포함할 수 없다.
- 아스키 제어 문자를 포함할 수 없다.
- **브랜치 이름은 중복해서 사용하지 않아야 한다.**

```bash
YuBeenSo@DESKTOP-SKBKL14 MINGW64 /c/coding/coding/2022 OSS/git/gitstudy06 (main)
$ git branch footer     # 바로 앞서서 만들었던 브랜치 이름을 그대로 사용하여 생성해 보았다.
fatal: a branch named 'footer' already exists     # 결과로 'footer'라는 이름의 브랜치는 이미 존재한다는 에러 문구가 뜬다.
```
<br/><br/>

## 6-3-3. 소스트리 브랜치
### 📌 소스트리로 새로운 브랜치 생성
1. 소스트리의 새 탭에서 **Add** 버튼을 클릭, 그 후 **탐색**을 눌러 앞서 만든 gitstudy06 폴더를 찾아 선택한 후 **추가** 클릭

![image](https://user-images.githubusercontent.com/99963066/194833006-73923b15-6c86-4b4b-a3d9-78c552053d0d.png)
<br/><br/>

2. **main 브랜치를 선택**하고 커밋 목록에서 **커밋을 하나 선택**하여 마우스 오른쪽 버튼을 눌러 **브랜치..** 메뉴를 선택하거나 위쪽에 있는 **브랜치 생성 버튼**을 클릭하    여 소스트리에 브랜치를 하나 추가한다.

![image](https://user-images.githubusercontent.com/99963066/194834549-494b2186-8212-4e74-9edd-dc23691892dc.png)
<br/><br/>

3. 브랜치.. 나 브랜치 생성 버튼을 클릭하면 다음과 같은 브랜치 생성 창이 열린다. 소스트리에서 **커밋을 선택**하여 브랜치를 생성하는 것은 **지정한 커밋을 기준으로 브랜치를 생성**한다는 의미이다. 커밋 목록에서 브랜치를 생성하면 **명시된 커밋** 부분에 브랜치가 체크되어 있는 것을 볼 수 있다. main의 최종 커밋(HEAD)을 기준으로 브랜치를 생성할 때는 **작업 사본 부모** 항목을 선택한다.

![image](https://user-images.githubusercontent.com/99963066/194836838-454f7591-1567-49d2-939d-af1ac45cfd0a.png)
<br/><br/>

4. 위에서 새로운 feature 브랜치를 하나 추가했다. 소스트리 왼쪽에서 추가한 브랜치인 feature를 볼 수 있다. 브랜치는 총 3개이고 현재 브랜치는 feature가 되는 것도 확인 가능하    다.

![image](https://user-images.githubusercontent.com/99963066/194837680-de540f96-d3e9-4f6e-a7bb-36d3339c6fdd.png)

# 6.9 원격 브랜치

🤝 깃은 다수의 개발자와 협업으로 코드를 유지할 수 있음

## 6.9.1 리모트 브랜치

💬 **리모트 브랜치**:원격 저장소에 생성한 브랜치 <br>
1. 원격 저장소와 로컬 저장소의 브랜치 이름을 보통 같지만 반드시 일치하지 않아도 가능하다. <br>
2. 리모트 브랜치는 보통 별칭/브랜치 이름 형태이다. <br>

## 6.9.2 실습 준비

### ⚡ 깃허브 실습 저장소에 New repository 클릭 후 새 저장소 생성
![실습1](https://user-images.githubusercontent.com/105197524/194878535-b499048e-8612-4f32-89ca-c6acb3a5f68a.png)

**새 저장소 생성 후 다음과 같이 실행**
```bash
$ git remote add origin 주소 ->원격 저장소 등록
$ git remote -v -> 원격 저장소 목록
```
![실습2](https://user-images.githubusercontent.com/105197524/194878543-353236e0-7cce-4fbe-a5cc-0de1a9d08af1.png)

## 6.9.3 브랜치 추적

## 🔭 브랜치 추적:원격 저장소 브랜치를 가리키는 것 다른 용어로 트래킹 브랜치 <br>
### 로컬 저장소는 마지막으로 연결된 리모트 브랜치의 커밋 해시 값을 항상 가지고 있음

## 6.9.4 브랜치 업로드

### ⚡ 등록된 원격 저장소의 리모트 브랜치는 remote show 명령어로 확인 가능
![실습3-1](https://user-images.githubusercontent.com/105197524/194880929-d806a7b2-ecdf-4933-bde6-2a66bfd3d5d0.png)

### ⚡ 로컬 저장소에서 main 브랜치를 전송하기
```bash
$ git push -u origin main -> main 브랜치 전송
$ git push -u origin hotfix -> hotfix 브랜치 전송
```
## 🔭 원격 저장소에 잘들어감
![실습4](https://user-images.githubusercontent.com/105197524/194878549-46a310ee-742a-4cad-a8d7-ef196bf9613d.png)


## 6.9.5 이름이 다른 브랜치

### ⚡  다른 개발자가 만든 원격 서버의 브랜치를 테스트하려고 할 때 자신의 브랜치 이름과 같으면 충돌이 발생한다.이때 브랜치를 직접 수동으로 지정할 때는 콜론(:)으로 구분한다.

```bash
$ git push -u origin feature:function -> 다른 이름으로 브랜치 전송
```
![실습5](https://user-images.githubusercontent.com/105197524/194878550-6bf29046-6bb4-423f-ac8a-0e7d23830521.png)

## 6.9.6 업스트림 트래킹

## 🔭 업스트림 트래킹:로컬 저장소의 브랜치와 원격 저장소의 브랜치를 업로드할 수 있도록 매칭되는 것

### ⚡ 새롭게 저장소를 복제
```bash
$ git clone https://github.com/uh004/gitstudy06.git gitstudy06_clone -> 복제
$ cd gitstudy06_clone -> 폴더 이동
$ git branch -v ->브랜치 목록
$ git branch -r -> 리모트 브랜치 목록
$ git branch -vv -> 트래킹 브랜치 목록
$ git checkout --track origin/function -> 업스트림 브랜치 생성
```
![실습6](https://user-images.githubusercontent.com/105197524/194878553-f06d0e18-c114-4191-a457-26c523e80a71.png)
```bash
$ code branch.htm -> 복제된 gitstudy06_clone의 function 브랜치를 수정합니다. 입력
```
### ⚡ 복제 저장소 -> 원격 저장소 push
![실습7](https://user-images.githubusercontent.com/105197524/194878557-d5f5bfbe-a10c-48e9-b324-27fceca75796.png)
### ⚡ 원격 저장소 -> 원본 저장소 pull
![실습8](https://user-images.githubusercontent.com/105197524/194878560-ab6656b5-db90-404b-b5cb-8505e1ac731c.png)


## 6.9.7 원격 브랜치 복사

### ⚡ 원격 저장소에 브랜치 aaa 생성
![제목 없음](https://user-images.githubusercontent.com/105197524/194883294-541e9504-ab48-4006-8de5-b347a2dc8ad6.png)
```bash
$ git fetch -> 브랜치 커밋 가져오기
$ git branch -r -> 원격 브랜치 확인
$ git checkout -b aaa origin/aaa -> 브랜치 생성 및 이동
$ code branch.htm -> 새로운 .... 작업을 합니다. 입력
$ git commit -am "testing aaa" -> 등록 및 커밋
$ git push -> 커밋 전송
```
![실습9](https://user-images.githubusercontent.com/105197524/194878561-d3c32b88-2821-4fb9-bd8c-0069ef283f6e.png)

## 6.9.8 업스트림 연결

### ⚡ 원격 저장소에 브랜치 bbb 생성
![실습10](https://user-images.githubusercontent.com/105197524/194878562-2e1f7ce0-7eb1-4614-9719-f3d0a01f6694.png)

```bash
$ git fetch ->서버의 브랜치 정보 갱신
$ git branch -r -> 원격 브랜치 목록
$ git checkout -b bug -> 브랜치 생성
$ git branch -vv -> 트래킹 브랜치 목록
$ git branch -u origin/bbb -> 업스트림 연결
$ git branch -vv ->트래킹 브랜치 목록
```
![실습11](https://user-images.githubusercontent.com/105197524/194878564-e8f425fb-0116-478c-827d-441ec0b363b1.png)

### 📄 로컬 저장소의 bug 브랜치가 원격 저장소에 있는 aaa 리모트 브랜치의 트래킹 브랜치로 업스트림 된것을 확인


