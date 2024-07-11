# 단일 서버에서 Gitlab + Gitlab Runner 환경 구축하기 [Setting up GitLab + GitLab Runner on a Single Server]

* Gitlab 은 docker compose 로 진행
  * 기존 사내 서버의 DB가 이미 docker compose 로 관리되고 있었고 쉬운 유지보수 
* Gitlab Tier 는 Gitlab Community Edition (CE) 가 아닌 Enterprise Edidiont (EE) 로 선택
  * EE 의 Core Tier 를 이용하면 무료로 사용할 수 있고 CE -> EE 보다 EE core -> EE standard 가 더 쉽기 때문에 굳이 CE를 이용할 필요가 없음. (즉, 추후 유료버전 사용이 쉽도록 EE core 선택)
  * Gitlab CE 오픈소스를 직접 커스텀 해서 사용할 일이 없고, 사내 인프라 용이기 때문에 굳이 오픈소스만 이용해야 할 이유가 없었음.

단점
- GitLab 자체 릴리즈 및 보안패치 주기적으로 확인 필요

장점
- 프로젝트 (레포) 마다 고유의 git 브랜치 전략 사용 가능
- 노션 대신 워크플로우 구성 가능
- 배포 파이프라인 구성 및 봇 사용 가능 

## Spec
- GitLab `16.11.6`
- GitLab Runner `16.11.2`

> [!IMPORTANT] <br>
> GitLab Runner 버전은 Gitlab 버전과 동일하게 맞춰야 합니다.
> Ref. https://docs.gitlab.com/runner/#gitlab-runner-versions


[추가 설정]
- SMTP 설정
  - https://www.bearpooh.com/116

docker-compose.yaml
```yaml
services:
  gitlab:
    image: gitlab/gitlab-ee:16.11.6-ee.0
    platform: linux/amd64
    container_name: ${INTERNAL_GITLAB_HOSTNAME}
    restart: always
    hostname: gitlab.bd
    environment:
      GITLAB_OMNIBUS_CONFIG: |
        external_url 'http://${INTERNAL_GITLAB_HOSTNAME}/gitlab/'
    networks:
      - gitlab-network
    ports:
      - '80:80'
      - '443:443'
      - '2222:22'
    volumes:
      - '${GITLAB_HOME}/config:/etc/gitlab'
      - '${GITLAB_HOME}/logs:/var/log/gitlab'
      - '${GITLAB_HOME}/data:/var/opt/gitlab'
    shm_size: '256m'

  gitlab-runner:
    image: 'gitlab/gitlab-runner:v16.11.2'
    container_name: gitlab-runner
    restart: unless-stopped
    depends_on:
      - gitlab
    networks:
      - gitlab-network
    volumes:
      - './runner/config:/etc/gitlab-runner'
      - '/var/run/docker.sock:/var/run/docker.sock'
    ports:
      - "8093:8093"
    expose:
      - "80"
networks:
  gitlab-network:
    driver: bridge
```

.env
```yaml
GITLAB_HOSTNAME=
GITLAB_HOME=
INTERNAL_GITLAB_HOSTNAME= # gitlab 과 gitlab runner 내부 통신용도로 쓰일 호스트명을 마음대로 지정해주세요. 도커이기 때문에 외부로 실제 외부에서 접근하는 도메인과는 다릅니다. 
```

## how to setup
1. 도커 띄우기
```shell
docker-compose up -d
```

2. GitLab 에 Gitlab Runner 등록

> 어떤 권한의 Gitlab Runner 로 등록할 것 인지 선택 후 이후 과정 진행.
> Ref. https://docs.gitlab.com/runner/#who-has-access-to-runners-in-the-gitlab-ui

저는 그룹에 상관없이 한개의 Gitlab Runner 로 모든 파이프라인을 구성할 것 이기 때문에, Instance Runner 사용했습니다.

