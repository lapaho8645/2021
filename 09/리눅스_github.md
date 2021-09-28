## git 저장소 등록
#### github 정보 등록
```c
git config --global user.name "계정 이름"
git config --global user.email "계정 이메일"
```
#### 저장소 생성
* 커밋하고자 하는 파일 디렉토리로 이동 후 입력
```c
git init
```
#### git 상태 확인
```c
git status
```
#### 원격 저장소 등록
```c
git remote add origin "자신의 저장소 주소"
git fetch origin
```
#### 원격 저장소 삭제
```c
git remote remove origin
```
## 변경 내용 커밋
#### 변경된 내용 확인
```c
git status
```
![image](https://user-images.githubusercontent.com/64197428/135056401-89325fda-0eb9-4acd-b9d4-0bfc9fb8b261.png)

#### 변경된 내용 add
```c
git add "파일 이름"
git add -A    //모든 파일
```
![image](https://user-images.githubusercontent.com/64197428/135056479-518d1a41-08f6-451f-bc8d-070d4808343d.png)

#### 저장소에 commit
```c
git commit -m "커밋 메시지"
```
![image](https://user-images.githubusercontent.com/64197428/135056542-d940d5c0-2279-4866-b513-8b0e8f6703cd.png)

#### 저장소로 push
```c
git push origin +master     //master 브랜치로 푸시
```
