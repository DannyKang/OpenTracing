# Jaeger HOTROD sample 

이 예제는 Jaeger의 Sample Application인 HOTROD에 대한 설명이다.

## 사전준비사항
 - Docker : https://runnable.com/docker/install-docker-on-windows-10
 - Go lang

 ### Jeager 실행
 ```bash
 $ sudo docker run -d --name jaeger \
-p 6831:6831/udp \
-p 16686:16686 \
-p 14268:14268 \
jaegertracing/all-in-one:1.6
```
### HOTROD 실행

```bash
$ sudo docker run --rm -it \
--link jaeger \
-p8080-8083:8080-8083 \
jaegertracing/example-hotrod:1.6 \
all \
--jaeger-agent.host-port=jaeger:6831

```

### Jeager 접속
http://localhost:16686/

### HOTROD 접속 
http://localhost:8080/


### Source로 실행하기
```bash
mkdir -p $GOPATH/src/github.com/jaegertracing
cd $GOPATH/src/github.com/jaegertracinggit 
clone git@github.com:jaegertracing/jaeger.git jaeger
cd jaeger
make install
cd examples/hotrod
go run ./main.go all
```


### Reference
[Take OpenTracing for a HotROD ride](https://medium.com/opentracing/take-opentracing-for-a-hotrod-ride-f6e3141f7941)

