# Docker Tutorial
도커 튜토리얼

# Tutorial 준비
- Docker Desktop이 설치된 PC

<img width="426" alt="스크린샷 2023-03-09 오후 1 46 54" src="https://user-images.githubusercontent.com/38535571/223919692-8b442574-fd95-49a9-a530-d94f613ddc9c.png">



# Tutorial 1 - 이미지 사용하기
#### 이미지 다운로드
```bash
[ec2-user@@ip-xxx-xxx-xxx-xxx ~]$ docker pull nginx
Using default tag: latest
latest: Pulling from library/nginx
66dbba0fb1b5: Pull complete
6a4b1f0b5a90: Pull complete
16ea4daad357: Pull complete
646b2422838c: Pull complete
c6036fb71e57: Pull complete
dc0e78f15ad0: Pull complete
Digest: sha256:aa0afebbb3cfa473099a62c4b32e9b3fb73ed23f2a75a65ce1d4b4f55a5c2ef2
Status: Downloaded newer image for nginx:latest
docker.io/library/nginx:latest
```
```bash
[ec2-user@@ip-xxx-xxx-xxx-xxx ~]$ docker pull redis
Using default tag: latest
latest: Pulling from library/redis
66dbba0fb1b5: Already exists
9e30abea72ba: Pull complete
d01ec855d06e: Pull complete
7f65636102fd: Pull complete
56f49543da32: Pull complete
60a641879ddf: Pull complete
Digest: sha256:e50c7e23f79ae81351beacb20e004720d4bed657415e68c2b1a2b5557c075ce0
Status: Downloaded newer image for redis:latest
docker.io/library/redis:latest
```
```bash
[ec2-user@@ip-xxx-xxx-xxx-xxx ~]$ docker pull ubuntu
Using default tag: latest
latest: Pulling from library/ubuntu
d0a4bfa485d1: Pull complete
Digest: sha256:2adf22367284330af9f832ffefb717c78239f6251d9d0f58de50b86229ed1427
Status: Downloaded newer image for ubuntu:latest
docker.io/library/ubuntu:latest
```
```bash
[ec2-user@@ip-xxx-xxx-xxx-xxx ~]$ docker pull ubuntu:20.04
20.04: Pulling from library/ubuntu
698acb83f45f: Already exists
Digest: sha256:9fa30fcef427e5e88c76bc41ad37b7cc573e1d79cecb23035e413c4be6e476ab
Status: Downloaded newer image for ubuntu:20.04
docker.io/library/ubuntu:20.04
```

#### 이미지 목록 확인하기
```bash
[ec2-user@ip-xxx-xxx-xxx-xxx ~]$ docker images
REPOSITORY   TAG       IMAGE ID       CREATED      SIZE
redis        latest    edf4b3932692   7 days ago   111MB
ubuntu       20.04     7ace790b8bce   8 days ago   65.7MB
nginx        latest    114aa6a9f203   8 days ago   135MB
ubuntu       latest    730eeb702b69   8 days ago   69.2MB
```

#### 이미지 삭제하기
```bash
[ec2-user@ip-xxx-xxx-xxx-xxx ~]$ docker rmi ubuntu:latest
Untagged: ubuntu:latest
Untagged: ubuntu@sha256:2adf22367284330af9f832ffefb717c78239f6251d9d0f58de50b86229ed1427
Deleted: sha256:730eeb702b69e53ae1c79541a48af6303d1bd240014dc6b4208ee4f3fab7b681
Deleted: sha256:90d6d7c9f66575093f7958c215f0b1e138c339c8e77406ca75c621117677d147
```

# Tutorial 2 컨테이너 사용하기


#### 컨테이너 실행하기
```bash
[ec2-user@ip-xxx-xxx-xxx-xxx ~]$ docker run ubuntu:20.04
```
```bash
[ec2-user@ip-xxx-xxx-xxx-xxx ~]$ docker run -d -p 1234:6379 redis
3758bb5c3c6214b0b5d0bc94c5ddca5284ceebe3f2c896a543ddd7f9ee2bb1cc
```
```bash
[ec2-user@ip-xxx-xxx-xxx-xxx ~]$ docker run nginx
/docker-entrypoint.sh: /docker-entrypoint.d/ is not empty, will attempt to perform configuration
/docker-entrypoint.sh: Looking for shell scripts in /docker-entrypoint.d/
/docker-entrypoint.sh: Launching /docker-entrypoint.d/10-listen-on-ipv6-by-default.sh
10-listen-on-ipv6-by-default.sh: info: Getting the checksum of /etc/nginx/conf.d/default.conf
10-listen-on-ipv6-by-default.sh: info: Enabled listen on IPv6 in /etc/nginx/conf.d/default.conf
/docker-entrypoint.sh: Launching /docker-entrypoint.d/20-envsubst-on-templates.sh
/docker-entrypoint.sh: Launching /docker-entrypoint.d/30-tune-worker-processes.sh
/docker-entrypoint.sh: Configuration complete; ready for start up
2023/03/09 11:22:01 [notice] 1#1: using the "epoll" event method
2023/03/09 11:22:01 [notice] 1#1: nginx/1.23.3
2023/03/09 11:22:01 [notice] 1#1: built by gcc 10.2.1 20210110 (Debian 10.2.1-6)
2023/03/09 11:22:01 [notice] 1#1: OS: Linux 5.15.49-linuxkit
2023/03/09 11:22:01 [notice] 1#1: getrlimit(RLIMIT_NOFILE): 1048576:1048576
2023/03/09 11:22:01 [notice] 1#1: start worker processes
2023/03/09 11:22:01 [notice] 1#1: start worker process 29
2023/03/09 11:22:01 [notice] 1#1: start worker process 30
2023/03/09 11:22:01 [notice] 1#1: start worker process 31
2023/03/09 11:22:01 [notice] 1#1: start worker process 32
2023/03/09 11:22:01 [notice] 1#1: start worker process 33
```
```bash
[ec2-user@ip-xxx-xxx-xxx-xxx ~]$ docker run --name webserver -d -p 8080:80 nginx
0c62dffab5402cc17d89658078253f69498aee20d414ba3427166dd6ced06de2
[ec2-user@ip-xxx-xxx-xxx-xxx ~]$ curl localhost:8080
<!DOCTYPE html>
<html>
<head>
<title>Welcome to nginx!</title>
<style>
html { color-scheme: light dark; }
body { width: 35em; margin: 0 auto;
font-family: Tahoma, Verdana, Arial, sans-serif; }
</style>
</head>
<body>
<h1>Welcome to nginx!</h1>
<p>If you see this page, the nginx web server is successfully installed and
working. Further configuration is required.</p>

<p>For online documentation and support please refer to
<a href="http://nginx.org/">nginx.org</a>.<br/>
Commercial support is available at
<a href="http://nginx.com/">nginx.com</a>.</p>

<p><em>Thank you for using nginx.</em></p>
</body>
</html>
```

#### 컨테이너 목록 확인하기
```bash
[ec2-user@ip-xxx-xxx-xxx-xxx ~]$ docker ps
CONTAINER ID   IMAGE          COMMAND                  CREATED          STATUS          PORTS                    NAMES
0c62dffab540   nginx          "/docker-entrypoint.…"   47 seconds ago   Up 47 seconds   0.0.0.0:8080->80/tcp     webserver
3758bb5c3c62   redis          "docker-entrypoint.s…"   4 minutes ago    Up 4 minutes    0.0.0.0:1234->6379/tcp   blissful_driscoll
0cc9779b708a   ubuntu:20.04   "/bin/sh"                7 minutes ago    Up 7 minutes                             zen_shtern
```

#### 컨테이너 중지하기
```bash
[ec2-user@ip-xxx-xxx-xxx-xxx ~]$ docker stop 3758bb5c3c62
3758bb5c3c62
```
```bash
[ec2-user@ip-xxx-xxx-xxx-xxx ~]$ docker stop 0cc9779b708a
0cc9779b708a
```
```bash
[ec2-user@ip-xxx-xxx-xxx-xxx ~]$ docker stop webserver
webserver
```

#### 컨테이너 재시작하기
```bash
[ec2-user@ip-xxx-xxx-xxx-xxx ~]$ docker restart webserver
webserver
```

#### 컨테이너 제거하기
```bash
[ec2-user@ip-xxx-xxx-xxx-xxx ~]$ docker rm 3758bb5c3c62
3758bb5c3c62
```

#### 컨테이너 로그 확인하기
```bash
[ec2-user@ip-xxx-xxx-xxx-xxx ~]$ docker logs webserver
/docker-entrypoint.sh: /docker-entrypoint.d/ is not empty, will attempt to perform configuration
/docker-entrypoint.sh: Looking for shell scripts in /docker-entrypoint.d/
/docker-entrypoint.sh: Launching /docker-entrypoint.d/10-listen-on-ipv6-by-default.sh
10-listen-on-ipv6-by-default.sh: info: Getting the checksum of /etc/nginx/conf.d/default.conf
10-listen-on-ipv6-by-default.sh: info: Enabled listen on IPv6 in /etc/nginx/conf.d/default.conf
/docker-entrypoint.sh: Launching /docker-entrypoint.d/20-envsubst-on-templates.sh
/docker-entrypoint.sh: Launching /docker-entrypoint.d/30-tune-worker-processes.sh
/docker-entrypoint.sh: Configuration complete; ready for start up
2023/03/09 11:26:34 [notice] 1#1: using the "epoll" event method
2023/03/09 11:26:34 [notice] 1#1: nginx/1.23.3
2023/03/09 11:26:34 [notice] 1#1: built by gcc 10.2.1 20210110 (Debian 10.2.1-6)
2023/03/09 11:26:34 [notice] 1#1: OS: Linux 5.15.49-linuxkit
2023/03/09 11:26:34 [notice] 1#1: getrlimit(RLIMIT_NOFILE): 1048576:1048576
2023/03/09 11:26:34 [notice] 1#1: start worker processes
2023/03/09 11:26:34 [notice] 1#1: start worker process 29
2023/03/09 11:26:34 [notice] 1#1: start worker process 30
2023/03/09 11:26:34 [notice] 1#1: start worker process 31
2023/03/09 11:26:34 [notice] 1#1: start worker process 32
2023/03/09 11:26:34 [notice] 1#1: start worker process 33
172.17.0.1 - - [09/Mar/2023:11:27:43 +0000] "GET / HTTP/1.1" 200 615 "-" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/110.0.0.0 Safari/537.36" "-"
2023/03/09 11:27:43 [error] 29#29: *2 open() "/usr/share/nginx/html/favicon.ico" failed (2: No such file or directory), client: 172.17.0.1, server: localhost, request: "GET /favicon.ico HTTP/1.1", host: "localhost:8080", referrer: "http://localhost:8080/"
172.17.0.1 - - [09/Mar/2023:11:27:43 +0000] "GET /favicon.ico HTTP/1.1" 404 555 "http://localhost:8080/" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/110.0.0.0 Safari/537.36" "-"
2023/03/09 11:29:34 [notice] 1#1: signal 3 (SIGQUIT) received, shutting down
2023/03/09 11:29:34 [notice] 30#30: gracefully shutting down
2023/03/09 11:29:34 [notice] 30#30: exiting
2023/03/09 11:29:34 [notice] 29#29: gracefully shutting down
2023/03/09 11:29:34 [notice] 33#33: gracefully shutting down
2023/03/09 11:29:34 [notice] 29#29: exiting
2023/03/09 11:29:34 [notice] 33#33: exiting
2023/03/09 11:29:34 [notice] 29#29: exit
2023/03/09 11:29:34 [notice] 30#30: exit
2023/03/09 11:29:34 [notice] 32#32: gracefully shutting down
2023/03/09 11:29:34 [notice] 33#33: exit
2023/03/09 11:29:34 [notice] 32#32: exiting
2023/03/09 11:29:34 [notice] 32#32: exit
2023/03/09 11:29:34 [notice] 31#31: gracefully shutting down
2023/03/09 11:29:34 [notice] 31#31: exiting
2023/03/09 11:29:34 [notice] 31#31: exit
2023/03/09 11:29:34 [notice] 1#1: signal 17 (SIGCHLD) received from 30
2023/03/09 11:29:34 [notice] 1#1: worker process 30 exited with code 0
2023/03/09 11:29:34 [notice] 1#1: signal 29 (SIGIO) received
2023/03/09 11:29:34 [notice] 1#1: signal 17 (SIGCHLD) received from 32
2023/03/09 11:29:34 [notice] 1#1: worker process 32 exited with code 0
2023/03/09 11:29:34 [notice] 1#1: signal 29 (SIGIO) received
2023/03/09 11:29:34 [notice] 1#1: signal 17 (SIGCHLD) received from 29
2023/03/09 11:29:34 [notice] 1#1: worker process 29 exited with code 0
2023/03/09 11:29:34 [notice] 1#1: worker process 31 exited with code 0
2023/03/09 11:29:34 [notice] 1#1: signal 29 (SIGIO) received
2023/03/09 11:29:34 [notice] 1#1: signal 17 (SIGCHLD) received from 31
2023/03/09 11:29:34 [notice] 1#1: signal 17 (SIGCHLD) received from 33
2023/03/09 11:29:34 [notice] 1#1: worker process 33 exited with code 0
2023/03/09 11:29:34 [notice] 1#1: exit
/docker-entrypoint.sh: /docker-entrypoint.d/ is not empty, will attempt to perform configuration
/docker-entrypoint.sh: Looking for shell scripts in /docker-entrypoint.d/
/docker-entrypoint.sh: Launching /docker-entrypoint.d/10-listen-on-ipv6-by-default.sh
10-listen-on-ipv6-by-default.sh: info: IPv6 listen already enabled
/docker-entrypoint.sh: Launching /docker-entrypoint.d/20-envsubst-on-templates.sh
/docker-entrypoint.sh: Launching /docker-entrypoint.d/30-tune-worker-processes.sh
/docker-entrypoint.sh: Configuration complete; ready for start up
2023/03/09 11:31:13 [notice] 1#1: using the "epoll" event method
2023/03/09 11:31:13 [notice] 1#1: nginx/1.23.3
2023/03/09 11:31:13 [notice] 1#1: built by gcc 10.2.1 20210110 (Debian 10.2.1-6)
2023/03/09 11:31:13 [notice] 1#1: OS: Linux 5.15.49-linuxkit
2023/03/09 11:31:13 [notice] 1#1: getrlimit(RLIMIT_NOFILE): 1048576:1048576
2023/03/09 11:31:13 [notice] 1#1: start worker processes
2023/03/09 11:31:13 [notice] 1#1: start worker process 22
2023/03/09 11:31:13 [notice] 1#1: start worker process 23
2023/03/09 11:31:13 [notice] 1#1: start worker process 24
2023/03/09 11:31:13 [notice] 1#1: start worker process 25
2023/03/09 11:31:13 [notice] 1#1: start worker process 26
```

#### 컨테이너 쉘로 접속하기
```bash
[ec2-user@ip-xxx-xxx-xxx-xxx ~]$ docker exec -it webserver /bin/bash
```

# Tutorial 3 이미지 생성하기

### spring-petclinic 다운로드
```bash
[ec2-user@ip-xxx-xxx-xxx-xxx ~]$ git clone https://github.com/spring-projects/spring-petclinic
[ec2-user@ip-xxx-xxx-xxx-xxx ~]$ cd spring-petclinic
```

#### Dockerfile 생성
```Dockerfile
# syntax=docker/dockerfile:1
FROM eclipse-temurin:17-jdk-jammy

WORKDIR /app

COPY .mvn/ .mvn
COPY mvnw pom.xml ./
RUN ./mvnw dependency:resolve

COPY src ./src

CMD ["./mvnw", "spring-boot:run"]
```

#### 이미지 빌드하기
```bash
[ec2-user@ip-xxx-xxx-xxx-xxx ~]$ docker build -t spring-petclinic:0.0.1 .
```

#### 이미지 확인하기
```bash
[ec2-user@ip-xxx-xxx-xxx-xxx ~]$ docker images
REPOSITORY         TAG       IMAGE ID       CREATED          SIZE
spring-petclinic   0.0.1     451aadfba421   22 seconds ago   553MB
redis              latest    edf4b3932692   7 days ago       111MB
ubuntu             20.04     7ace790b8bce   8 days ago       65.7MB
nginx              latest    114aa6a9f203   8 days ago       135MB
```

#### 이미지 실행하기
```bash
[ec2-user@ip-xxx-xxx-xxx-xxx ~]$ docker run -p 1234:8080 spring-petclinic:0.0.1
```
<img width="1414" alt="스크린샷 2023-03-09 오후 9 04 36" src="https://user-images.githubusercontent.com/38535571/224021576-0d989cfa-50a2-48f0-b5cb-11c9d7bd2cf8.png">


# Tutorial 4 이미지 배포하기 (DockerHub 계정 및 연동 필요)

#### 로그인
```bash
[ec2-user@ip-xxx-xxx-xxx-xxx ~]$ docker login
```

#### 이미지 태그 변경
```bash
[ec2-user@ip-xxx-xxx-xxx-xxx ~]$ docker image tag spring-petclinic:0.0.1 [DockerHub]/spring-petclinic:0.0.1
```

#### 이미지 업로드하기

```bash
[ec2-user@ip-xxx-xxx-xxx-xxx ~]$ docker push [DockerHub]/spring-petclinic:0.0.1
```
<img width="1281" alt="스크린샷 2023-03-09 오후 9 16 28" src="https://user-images.githubusercontent.com/38535571/224021588-4307d2db-6f4e-4677-a0ff-afb9ab8820b9.png">
