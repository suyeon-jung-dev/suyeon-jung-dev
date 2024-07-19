# Accessing the ChaosCenter

### minikube 에서 바로 접근하기

1. 서비스 명 조회
```shell
kubectl get svc -n litmus
```

예시
```shell
➜  ~ kubectl get svc -n litmus
NAME                               TYPE        CLUSTER-IP       EXTERNAL-IP   PORT(S)             AGE
chaos-litmus-auth-server-service   ClusterIP   10.110.179.175   <none>        9003/TCP,3030/TCP   30m
chaos-litmus-frontend-service      NodePort    10.101.143.230   <none>        9091:31932/TCP      30m
chaos-litmus-server-service        ClusterIP   10.110.202.253   <none>        9002/TCP,8000/TCP   30m
chaos-mongodb-arbiter-headless     ClusterIP   None             <none>        27017/TCP           30m
chaos-mongodb-headless             ClusterIP   None             <none>        27017/TCP           30m
```

2. 접속하고 싶은 서비스 명으로 접속. 터미널을 열어 둔 동안에만 접속 가능합니다. 
```shell
minikube service <SERVICE-ID> -n litmus
```

예시
```shell
➜  ossca minikube service chaos-litmus-frontend-service -n litmus
|-----------|-------------------------------|-------------|---------------------------|
| NAMESPACE |             NAME              | TARGET PORT |            URL            |
|-----------|-------------------------------|-------------|---------------------------|
| litmus    | chaos-litmus-frontend-service | http/9091   | http://192.168.49.2:31932 |
|-----------|-------------------------------|-------------|---------------------------|
🏃  chaos-litmus-frontend-service 서비스의 터널을 시작하는 중
|-----------|-------------------------------|-------------|------------------------|
| NAMESPACE |             NAME              | TARGET PORT |          URL           |
|-----------|-------------------------------|-------------|------------------------|
| litmus    | chaos-litmus-frontend-service |             | http://127.0.0.1:55806 |
|-----------|-------------------------------|-------------|------------------------|
🎉  Opening service litmus/chaos-litmus-frontend-service in default browser...
❗  darwin 에서 Docker 드라이버를 사용하고 있기 때문에, 터미널을 열어야 실행할 수 있습니다
```

