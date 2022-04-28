# AWS연결방법

프리티어로 EC2 생성

## 보안그룹

#### 보안그룹 인바운드 설정
- 80 
- 8080
- 3306
- 22 ( 자기 아이피만 사용할 것 , ::0 으로 만들면 다른 사람이 접속할 수 있음

#### RDS 보안그룹 인바운드 설정
- EC2 오픈


## PUTTY 설정

#### 아이피 설정 
![putty](https://user-images.githubusercontent.com/64408793/165507106-d658146d-41e3-4ffb-b6c7-916aaf0c9848.png)

#### ppk 파일 등록 후 확인

![image](https://user-images.githubusercontent.com/64408793/165507192-2b27bc05-9ee3-440b-b707-d1aa82beae4f.png)

#### 푸티 업그레이드
- sudo apk-get update
- sudo apk-get upgrade

#### 푸티 자바 설치
- sudo apt-get install openjdk-8-jre ( jre )
- sudo apt-get install openjdk-8-jdk ( jdk ) 
- 자바 버전확인 : java -version
- 자바c 버전    : javac -version

![image](https://user-images.githubusercontent.com/64408793/165657185-c45ad3e4-c661-4dc1-81ac-ed736ee9d884.png)


- 자바 나노 편집기 : sudo nano /etc/profile
 자바 설정을 잡아야함
 
 - putty 저장 : ctrl + o 후 엔터
 - putty 나오기 : ctrl + x
 - export 3가지 입력 후 저장
 export JAVA_HOME=/usr/lib/jvm/java-8-openjdk-amd64
 export PATH=$JAVA_HOME/bin/:$PATH
 export CLASS PATH=$JAVA_HOME/lib:$CLASS_PATH
 
 ( 만약 오타가 발생해 어떠한 명령어도 듣지 않는다면
 export PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin 를 입력

![image](https://user-images.githubusercontent.com/64408793/165513657-d77e8e63-b477-4289-b6bb-1477956afd41.png)
 
 - 입력 후 source /etc/profile 로 reload 를 해주고
 - sudo reboot now 로 서버 재부팅을 한다.
 - 서버 재부팅 후 echo $JAVA_HOME 와 $JAVA_HOME/bin/javac -version 을 입력해 경로가 잘 입력되었는지 확인
 
 #### 푸티 톰캣설치
 
- sudo apt-get install tomcat8
- sudo /usr/share/tomcat8/bin/version.sh 을 쳐서 톰캣 버전 확인
- sudo ufw allow 8080/tcp 포트번호 변경
- sudo service tomcat8 start 로 시작!
- 아래 화면이 뜨면 성공
![image](https://user-images.githubusercontent.com/64408793/165518026-0b6c5b76-d24e-47b6-9e84-88206702a349.png)


#### 배포
![image](https://user-images.githubusercontent.com/64408793/165518092-54689f78-1708-48a2-94e0-1673ac027952.png)


- vi /var/lib/tomcat7/conf/server.xml 로 톰캣 설정 변경 ( 만약 파일 로드했지만 읽히지 않는다면 권한 문제 sudo chmod 646 server.xml 를 입력해 권한 변경 )
- nano server.xml 를 들어간 후 아래 사진과 같이 코드 수정

![image](https://user-images.githubusercontent.com/64408793/165521041-cfd264c4-91fc-45c3-81e0-abcf4aa5381b.png)


- war 파일 export 
- 톰캣 권한 변경   ~ $ sudo su
- chmod -R 777 /var/lib/tomcat8/webapps
- chown -R tomcat8:tomcat8 /var/lib/tomcat8/webapps
- /var/lib/tomcat8/webapps 폴더 밑에 war 파일을 전송
- sudo chmod -R 777 경로 또는 파일 로 권한 변경 


#### AWS 요금이 발생하는 이유

- 프리티어로 만들지 않음
- 탄력적 IP (Elastic IP ) 를 연결하지 않음
- 탄력적 IP 요금관련 내용

![image](https://user-images.githubusercontent.com/64408793/165655598-8576dce7-b239-4a34-ae41-9d4732729ae9.png)



