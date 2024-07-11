# GitLab Runner 설치하기

> GitLab Runner 버전은 Gitlab 버전과 동일하게 맞춰야 합니다.
> Ref. https://docs.gitlab.com/runner/#gitlab-runner-versions

gitlab-runner 버전 : `v16.11.2` 사용. 배포날짜 `Jul 6, 2024`
Ref. [docker-hub](https://hub.docker.com/layers/gitlab/gitlab-runner/v16.11.2/images/sha256-6496da73785b6d8312207230cec81a257bec5825dc072d0861340ac4066ff578?context=explore)

1. docker compose 디렉토리 생성
```shell
mkdier gitlab-runner
```

2. 디렉토리 소유권 부여
```shell
sudo chown -R $USER:$USER ./gitlab-runner
```

3. docker-compose.yml 파일 생성 <br>
[docker-compose.yml](docker-compose.yml)

4. 실행
```shell
docker-compose up -d
```

# GitLab 에 Gitlab Runner 등록

> 어떤 권한의 Gitlab Runner 로 등록할 것 인지 선택
> Ref. https://docs.gitlab.com/runner/#gitlab-runner-versions

저는 그룹에 상관없이 한개의 Gitlab Runner 로 모든 파이프라인을 구성할 것 이기 때문에, Instance Runner 사용
