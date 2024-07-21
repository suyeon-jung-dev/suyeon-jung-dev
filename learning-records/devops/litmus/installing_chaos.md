# Installing Listmus Chaos

## 필요 스펙
- Minikube
- Helm3

### 사전 조건
- docker engine install
- minikube : https://minikube.sigs.k8s.io/docs/start/?arch=%2Fmacos%2Farm64%2Fstable%2Fhomebrew
- litmus pre-requisites: https://docs.litmuschaos.io/docs/getting-started/installation/#prerequisites
    - helm3: https://helm.sh/docs/intro/install/#from-homebrew-macos
    - kubectl: https://kubernetes.io/docs/tasks/tools/install-kubectl-macos/#install-with-homebrew-on-macos

### helm 으로 litmus 설치 : https://docs.litmuschaos.io/docs/getting-started/installation#install-litmus-using-helm
   - minikube 가 start 된 상태여야 이후 kubectl 로 네임스페이스를 지정 할 수 있습니다.
      ```shell
       ➜ ossca minikube start
       😄  Darwin 13.6.3 (arm64) 의 minikube v1.33.1
       ✨  기존 프로필에 기반하여 docker 드라이버를 사용하는 중
       👍  Starting "minikube" primary control-plane node in "minikube" cluster
       🚜  Pulling base image v0.0.44 ...
       🔄  Restarting existing docker container for "minikube" ...
       🐳  쿠버네티스 v1.30.0 을 Docker 26.1.1 런타임으로 설치하는 중
       🔎  Kubernetes 구성 요소를 확인...
       ▪ Using image gcr.io/k8s-minikube/storage-provisioner:v5
       🌟  애드온 활성화 : default-storageclass, storage-provisioner
       🏄  끝났습니다! kubectl이 "minikube" 클러스터와 "default" 네임스페이스를 기본적으로 사용하도록 구성되었습니다.
        ```
1. litmuschaos helm repo 추가
```shell
helm repo add litmuschaos https://litmuschaos.github.io/litmus-helm/
```
helm repo 잘 받아졌는지 확인
```shell
helm repo list
```

2. 네임스페이스 지정
```shell
➜  ossca kubectl create ns litmus
namespace/litmus created
```

2. 네임스페이스 목록 확인
```shell
➜  ossca kubectl get ns
NAME              STATUS   AGE
default           Active   17h
kube-node-lease   Active   17h
kube-public       Active   17h
kube-system       Active   17h
litmus            Active   17s
```

3. ARM 기반 MondoDB 로 이미지 변경하여 ChaosCenter 설치
```shell
➜  ossca helm install chaos litmuschaos/litmus --namespace=litmus \
--set portal.frontend.service.type=NodePort \
--set mongodb.image.registry=ghcr.io/zcube \
--set mongodb.image.repository=bitnami-compat/mongodb \
--set mongodb.image.tag=6.0.5
```

아웃풋은 다음과 같이 확인
```shell
NAME: chaos
LAST DEPLOYED: Fri Jul 19 10:48:39 2024
NAMESPACE: litmus
STATUS: deployed
REVISION: 1
TEST SUITE: None
NOTES:
Thank you for installing litmus 😀

Your release is named chaos and it's installed to namespace: litmus.

Visit https://docs.litmuschaos.io to find more info.
```

MondoDB를 포함하여 각 파드들이 정상적으로 동작하고 있는지 확인
```shell
➜  ossca kubectl get pods -n litmus
NAME                                       READY   STATUS     RESTARTS     AGE
chaos-litmus-auth-server-8499fc4cf-cxdgk   0/1     Init:0/1   0            3m57s
chaos-litmus-frontend-6fd8ff8b48-8kvwn     1/1     Running    0            3m57s
chaos-litmus-server-5484b76bc-zf7gw        0/1     Init:0/1   0            3m57s
chaos-mongodb-0                            1/1     Running    0            3m57s
chaos-mongodb-1                            1/1     Running    0            3m15s
chaos-mongodb-2                            1/1     Running    0            3m2s
chaos-mongodb-arbiter-0                    0/1     Running    1 (7s ago)   3m57s
```

> 혹시나 ARM 지원하는 MongoDB 이미지로 설정하지 않아 정상 동작하지 않는다면..
```shell
➜  ossca kubectl get pods -n litmus
NAME                                       READY   STATUS             RESTARTS         AGE
chaos-litmus-auth-server-8499fc4cf-2mlwt   0/1     Init:0/1           0                16h
chaos-litmus-frontend-6fd8ff8b48-jm22h     1/1     Running            0                16h
chaos-litmus-server-5484b76bc-mww4p        0/1     Init:0/1           0                16h
chaos-mongodb-0                            0/1     CrashLoopBackOff   51 (4m1s ago)    16h
chaos-mongodb-1                            0/1     CrashLoopBackOff   49 (3m58s ago)   16h
chaos-mongodb-2                            0/1     CrashLoopBackOff   47 (4m13s ago)   12h
chaos-mongodb-arbiter-0                    1/1     Running            17 (3m27s ago)   16h
```

기존에 생성한 namespace 제거
- namepace 목록 확인
    ```shell
    ➜  ossca kubectl get namespaces
    NAME              STATUS   AGE
    default           Active   17h
    kube-node-lease   Active   17h
    kube-public       Active   17h
    kube-system       Active   17h
    litmus            Active   16h
    ```
- 앞서 지정했던 litmus 라는 이름의 네임스페이스 제거
    ```shell
    ➜  ossca kubectl delete ns litmus
    namespace "litmus" deleted
    ```    
위에 정의된 ARM 지원하는 MongoDB 이미지로 재설치

> 이래도 안되면.. helm repo 에서 litmuschaos 도 삭제 후 다시 시도 해보시면 됩니다.
```shell
helm repo remove litmuschaos
```


