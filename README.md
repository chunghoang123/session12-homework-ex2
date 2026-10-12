# Session 12 - Ex2: Release Docker Image theo Git Tag

## Muc tieu
Khi gan tag `v*.*.*` thi tu dong build + push Image len GHCR voi tag tuong ung.

## Workflow `.github/workflows/release.yml`
- Trigger: `on.push.tags: ['v*.*.*']`.
- `docker/metadata-action@v5` trich xuat tag semver tu Git tag.
- `docker/build-push-action@v5` voi `context: .`, `file: ./Dockerfile`, day len `ghcr.io/<owner>/<repo>`.
- Quyen: `packages: write`.

## Dockerfile
Multi-stage: `eclipse-temurin:17-jdk` build `bootJar`, `eclipse-temurin:17-jre` chay app cong 8080.

## Kiem tra
```bash
git tag v1.0.0
git push origin v1.0.0
```
1. Mo tab **Actions** -> workflow `Release Docker Image on Git Tag` chay xanh.
2. Mo **Packages** (hoac trang package cua repo) thay `ghcr.io/...:v1.0.0`.
3. Chup man hinh de nop bai.

## Chay local
```bash
./gradlew test
docker build -t session12-ex2:local .
docker run -p 8080:8080 session12-ex2:local
curl http://localhost:8080/actuator/health
```
