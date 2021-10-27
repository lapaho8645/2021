## Unable to open swp file for "filename", recovery impossible
파일을 열 때마다 해당 오류 발생

메모리 공간이 부족하거나 편집 이력이 있었던 파일의 스왑 파일을 열지 못하여 발생하는 문제

![image](https://user-images.githubusercontent.com/64197428/139016409-9e614e91-7004-41c1-8022-b8da9a82c459.png)
#### 해결 방안
리눅스 시스템의 용량을 많이 차지하는 파일, 디렉토리를 찾아 정리
- 현재 파일 시스템 확인
```
df -h
```
> ![image](https://user-images.githubusercontent.com/64197428/139016892-1ca4dfe4-f5b9-449a-984f-15aeb0bc103b.png)
> 
> 루트 영역이 100% 사용하고 있음을 확인
- 용량을 많이 차지하는 파일, 디렉토리 찾기
```
du -sh * | sort -hr
```
> ![image](https://user-images.githubusercontent.com/64197428/139017435-49d89d3a-2177-4862-ad7a-817d9288600f.png)
> 
> dra 폴더에서 가장 많은 용량을 차지하고 있음을 확인
```
cd dra
du -sh * | sort -hr
```
> ![image](https://user-images.githubusercontent.com/64197428/139017773-04936145-6f83-4df7-a5e5-2439880ff066.png)
> 
> log 폴더에서 가장 많은 용량을 차지하고 있음을 확인

- 불필요한 파일 삭제
- 삭제 후 파일 시스템 확인

![image](https://user-images.githubusercontent.com/64197428/139018158-ff8416e9-a1cc-460c-b744-a01fcdf1a602.png)
