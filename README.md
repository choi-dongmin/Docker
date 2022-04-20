# Docker
- 우리는 하나의 애플리케이션을 만들때 여러 소프트웨어가 필요하다 예컨데 웹서버 소프트웨어, 데이터베이스 등 처럼

- 이처럼 여러 소프트 웨어를 가지고 우리는 애플리케이션을 만들고 유지하는데 이것을 설치하는것은 여간 까다로운것이 아닐 뿐더러 여러번 설치해야 한다면 더욱더 까다롭다.

* 만약 각각의 운영체제 & 소프트웨어들(데이터 베이스 설치 유지에 필요한 것/ 웹서버 설치 유지에 필요한 것)을 각각의 컴퓨터에서 설치를 하고 그것을 네트워크를 통해서 사용한다면 더 편할것이다.

- 하지만 비용적인 측면에서 본다면 위와같은 방법으로 할때 당장 컴퓨터가 3대가 필요하다.

* 그렇다면 만약 하나의 컴퓨터에 다른 컴퓨터 "가상의 컴퓨터" 를 만들수 있다면 비용적 측면에서 크게 절감할 수 있다.

- 하지만 위와 같은 방법으로 진행한다면 운영체제 위에 가상의 컴퓨터에 또 다른 운영체제를 설치함으로 속도, 용량 등에서 현저하게 느려진다.

- 그렇다면 만약 하나의 컴퓨터, 운영체제에서 소프트웨어를 실행시킨다면? 이건 처음 우리가 맞이한 문제와 다르지 않다.

* 하지만 그 소프트웨어들을 각각 하나의 격리된 환경에서 실행시킨다면?

- 하나의 운영체제 안의 각각 격리된 환경에서 "운영체제를 설치할 필요없이" 소프트웨어 실행에 필요한 프로그램만을 설치한다면 위와 같은 문제를 해결 할 수 있을것이다.

* 그래서 우리는 운영체제가 설치된 컴퓨터를 "host" 라고 하고 각각 소프트웨어들이 설치된 격리된 환경을 "container" 라고 일컫는다.

* 리눅스 운영체제에선 위와같 실행방법이 내장되어 있다 이런한 기술을 container 이다.

- 이와같은 container 기술 이용을 더 쉽게해주는 프로그램들이 있는데 그 중 "Docker" 를 배울것이다.

## 개념

- 우리가 만약 프로그램이 필요하면 app store 를 이용한다.

* Docker 는 "Docker Hub" 이라 레지스트리 라고 불리는 서비스에서 찾게 된다.

- 우리는 다운받아서 컴퓨터에 저장한 앱을 우리는 프로그램이라고 한다.

* 만약 Docker Hub 에서 필요한 것들을 다운받는것을 "pull"이라고 하고 도커에 저장한 것을 우리는 "image" 라고 한다.

- 프로그램을 실행시키면 프로세스가 실행된다.

* image 를 실행하면 "container" 가 실행된다.

## pull

- Docker Hub 에서 웹 서비스 프로그램(appach) image 를 Docker에 pull 할것이다. [Docker Hub](https://hub.docker.com/_/httpd)

* pull 을 위한 명령어는
```
docker pull [OPTIONS] NAME[:TAG|@DIGEST]
```
 - docker pull name 위와 같은 형식으로 이루어진.  [docs.docker.com](https://docs.docker.com/engine/reference/commandline/pull/)

 ```
 docker pull httpd
 ```
- 아파치를 docker 에 pull 하는 형식

* 만약 pull 한것을 확인하고 싶다면

```
docker images
```

위와같은 명령어로 지금 docker 에 어떤 image 들이 있는지 알 수 있다.

## rmi

- image 를 삭제하고 싶다면 rmi 명령어를 사용한다.
- rmi 명령 [docs.docker.com](https://docs.docker.com/engine/reference/commandline/rmi/)

```
 docker rmi [OPTIONS] IMAGE [IMAGE...]
```

- image httpd 를 삭제해보자.
```
 docker rmi httpd
```
## run

- Docker 안에 pull 을 했다면 이제 run 을 해야한다.
```
docker run [OPTIONS] IMAGE [COMMAND] [ARG...]
```
- docker run image 형식이다. [docs.docker.com](https://docs.docker.com/engine/reference/commandline/run/)


* httpd image 를 run 한다
```
Docker run httpd
```


* container 이름을 명령으로 지정할 수 있다.
```
Docker run --name WS httpd
```
- WS 라는 이름의 container 생성

* 만든 컨테이너들을 확인하고 싶다면 ps 명령을 실행한다.
```
docker ps [OPTIONS]
```
- containers 확인 [docs.docker.com](https://docs.docker.com/engine/reference/commandline/ps/)


## stop

- 실행중인 container 를 정지하고 싶다면 stop 명령어를 사용한다.

- stop 명령 [docs.docker.com](https://docs.docker.com/engine/reference/commandline/ps/)
```
docker stop [OPTIONS] CONTAINER [CONTAINER...]
```

- 기존에 있던 container WS 를 정지 해보자.
```
Docker stop WS
```

* 확인하고 싶다면 docker ps 를 사용하면된다 그러나 뒤에 -a 라는 명령어를 사용해야 확인 할 수 있다.

```
docker ps -a
```
- containers 확인 [docs.docker.com](https://docs.docker.com/engine/reference/commandline/ps/)

## start

- 정지중인 container 를 실행하고 싶다면 start 명령어를 사용한다.

- start 명령 [docs.docker.com](https://docs.docker.com/engine/reference/commandline/start/)
```
 docker start [OPTIONS] CONTAINER [CONTAINER...]
```

- 기존에 있던 container WS 를 시작해 보자.
```
Docker start WS
```

* 확인하고 싶다면 docker ps 를 사용하면 된다.

```
docker ps
```
- containers 확인 [docs.docker.com](https://docs.docker.com/engine/reference/commandline/ps/)

* 하지만 run 할때와는 다르게 logs 를 보여주지 않고 바로 실행된다.
- logs 를 보고 확인하고 싶다면 docker logs 명렬어를 사용한다.
- logs 확인 [docs.docker.com](https://docs.docker.com/engine/reference/commandline/logs/)
```
docker logs [OPTIONS] CONTAINER
```

- 다시 시작한 WS 로그 확인
```
docker logs WS
```
- 만약 실시간 로그를 확인 하고 싶다면 -f 명령어 사용

```
docker logs -f CONTAINER

docker logs -f WS
```

## rm
- container를 삭제하고 싶다면 rm 명령어 사용
- rm 명령 [docs.docker.com](https://docs.docker.com/engine/reference/commandline/rm/)

```
docker rm [OPTIONS] CONTAINER [CONTAINER...]
```

- WS container 삭제
```
docker rm WS
```

* 도커가 실행중이라면 끄고 삭제해야한다. 혹은 -force 명령어 삽입

## docker network
- 한 컴퓨터 아파치를 통해서 웹서버를 구축하고 "file system(웹 파일 저장공간)"에 경로를 지정해서 보여주게 되면 기본 port 는 80 이다.

- 만약 위 웹의 도메인이 ex1.com 이라면 ex1.com:80/index.html 라고 입력하면 80번 기본포트를 통해 index 를 불러온다.

* 그러나 만약 docker 에서 아파치 웹서버를 구축한다면 컴퓨터가 아닌 container 에 위치하게 된다.

* 이 container가 설치된 운영체제를 host 라고 한다.

* 이 host 는 각자 "독립적인 port" , "독립적인 file system"를 같게 된다.

* host 기본 포트 80, 아파치 기본 포트 80 같은 80번 포트지만 서로 이어주지 않으면 불러올 수 없다.

* 이때 container 를 실행할때 80 번 포트를 명령어를 통해 서로 이어준다
```
docker run -p 80:80 httpd

80(host):80(container)
```

* 이렇게 host 와 container 의 포트를 이어주는것을 "port forwarding" 이라고 한다.

### port forwarding
```
docker run -p 8080:80 httpd
```
- host 8080 을 통해 container 80 으로 이어준다.

- localhost:8080 과 docker logs 를 통해 확인 할 수 있다.


## 명령어를 통한 container 수정
- 명령어 프롬프트 혹은 터미널에서 continer 의 file system 수정하는 방법을 알아보자.
- exec 명령 [docs.docker.com](https://docs.docker.com/engine/reference/commandline/exec/)
```
docker exec [OPTIONS] CONTAINER COMMAND [ARG...]

```

* docker exec 컨테이너이름 명령어 를 입력한다면 continer 안에서 명령이 실행된다.
* 예를들어 docker exec ws ls 라고 입력한다면 ws 컨테이너 속에 있는 파일을 보여준다.
- 하지만 우리가 컨테이너와 지속적으로 연결을 유지하면서 명령을 하고 싶다면 조금 다르게 명령을 해야한다.

```
docker exec ws -ti /bin/sh or bash
```
* sh 혹은 bash 를 입력하게 된다면 shell 이라는 프로그램을 실행한다 shell 은 일종의 창구로 사용자의 명령을 받아서 운영체제한테 전달한다.

- 위의 코드를 실행하면 # 이 생기고 리눅스 명령어를 바로 continer 에 적용시킨다.  

* 명령어 -ti 를 사용했는데 이는 -t -i 각각의 명령어로 컨테이너와 명렴 프롬프트를 지속적으로 연결을 유지하면서 명령을 한다.

- appach 에서 제공하는 파일 저장 경로는 appach2/htdocs 이다.

```
1
docker exec ws -ti /bin/bash

```
```
2
root@c0ed5308b205:/usr/local/apache2# ls
bin  build  cgi-bin  conf  error  htdocs  icons  include  logs  modules

3
root@c0ed5308b205:/usr/local/apache2# cd htdocs

4
root@c0ed5308b205:/usr/local/apache2/htdocs# ls
index.html

5
root@c0ed5308b205:/usr/local/apache2/htdocs# nano index.html
bash: nano: command not found
```
* 1 bash 혹은 shell 을 통해 continer 에 지속적 연결
* 2 bash 를 사용중인 상태에서 현재 폴더 파일들  확인
* 3 appach 에서 제공하는 파일 저장 경로 htdocs 으로 이동
* 4 htdocs 폴더 파일 확인
* 5 nano 를 통해 index.html 실행(continer 는 가볍게 유지시키려 하기 때문에 실행프로그램 [nano] 가 존재하지 않음)

- 그렇다면 apt 를 이용해 실행파일 nano 를 continer에 깔아보자.
```
root@c0ed5308b205:/usr/local/apache2/htdocs# apt update
```
- apt 를 최신화 시키고

```
root@c0ed5308b205:/usr/local/apache2/htdocs# apt install nano
```
- nano install
```
root@c0ed5308b205:/usr/local/apache2/htdocs# nano index.html
<html><body><h1>It works!</h1></body></html>
```
- index.html 실행 완료

## 호스트와 컨테이너 파일 시스템 연결
- continer 이점은 용도에 따라 설치와 삭제가 가볍다는것이다.
* 만약 continer 를 삭제해야 하는 상황이 온다면 그간 continer 안쪽에 수정한 파일을 백업하는것도 굉장히 귀찮은 일이다.

* 그렇다면 우리는 이 문제를 host 에있는 file system과 continer의 file system을 연결시켜 host 에서 수정을 하면 container 에서 동시에 수정이 된다면 continer를 지우더라도 백업이 저절로 되고 다른 continer 를 만들어 연결시켜도 문제가 없을것이다.

* 이떄 -v 명령어를 run (continer 생성) 할때 host index.html 경로와 continer index.html 경로를 입력해주면 매칭된다.

```
docker run --name test -p 8080:80 -v C:\Users\이름\Desktop\htdocs:/usr/local/apache2/htdocs/ httpd


docker(도커를)
run(실행한다)
--name(이름명령) test
-p(포트명령) 8080:80
-v(볼륨명령[호스트 경로]:[컨테이너 경로]) C:\Users\이름\Desktop\htdocs:/usr/local/apache2/htdocs/
httpd
```   
- 위와 같은 방법으로 host file system과 container file system을 매칭시킬수 있다.

## 키워드
- Docker Hub : 도커의 images 를 pull 하기 쉽도록 모아놓은 허브.
- Image : 컴퓨터 안에 프로그램들이 있다면 , 도커 안에는 image들이 있다.
- Container : image 를 실행시킬 시 동작하는것 (EX 프로그램의 프로세스), 각각 소프트웨어들이 설치된 격리된 환경
- host : 운영체제가 깔린 컴퓨터
- Port Forwarding : 운영체제가 깔린 컴퓨터와 각각 소프트웨어가 설치된 격리된 환경 즉 , container 와 host 의 port 를 매칭 해주는것.

## 참고
[생활코딩](https://opentutorials.org/course/4781/30609)
