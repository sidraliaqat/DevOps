# Lab 5: Build, Test, and Package Applications with IntelliJ IDEA and Docker

| Field | Value |
|---|---|
| Name | SIDRA LIAQAT |
| Registration No | 2023-BCS-083 |
| Course / Section | DEVOPS/A |
| GitHub Username | sidraliaqat |
| Host login | sidraliaqat@ubuntu |

## Folder Contents

```
Labs/Lab05/
├── README.md
├── Lab5_Solution.pdf
└── screenshots/   (37 PNG files)
```

- `Lab5_Solution.pdf` has the task headings, screenshots in task order, a short caption for each, and the practice answers.
- `screenshots/` has all 37 required screenshots with the exact filenames from the lab.

## Environment

- Host: Ubuntu 26.04 LTS running in VMware Workstation (6 GB RAM, 6 GB swap file)
- IntelliJ IDEA 2026.2.3 running in Docker (browser desktop at https://192.168.44.128:3001)
- Container limits: 4 GB memory, 8 GB memory plus swap, 1.8 CPUs
- Docker 29.9.3, Maven (apt), Gradle Wrapper 7.0 on Temurin JDK 16.0.2, Node.js v22.23.4, npm 10.9.9

## Task 1: Clone and Launch IntelliJ IDEA

- Cloned `https://github.com/WaqasSaleem97/Intellij-Idea-docker.git` on the Ubuntu host.
- Ran `bash setup.sh` and `docker compose ps`, then opened the desktop on port 3001.
- Launched IntelliJ IDEA and reached the Welcome screen.
- Screenshots: `intellij_repo_clone.png`, `intellij_running.png`, `intellij_desktop.png`

## Task 2: Maven Project (java-maven-app)

- Cloned `https://gitlab.com/nanuchi/java-maven-app.git` into `/config/IdeaProjects/java-maven-app`.
- Installed Maven with `sudo apt install -y maven` and checked `mvn --version`.
- Ran `mvn package`, added `org.elasticsearch:elasticsearch:7.0.0` to `pom.xml`, synced Maven, then ran `mvn package` again and `mvn test`.
- Found `target/java-maven-app-1.1.0-SNAPSHOT.jar` and ran it with `java -jar`. Tomcat started on port 8080. Stopped it with Ctrl+C and closed the project.
- Problem and fix: the Elasticsearch dependency pulled in an old `jackson-core`, and the JAR failed with `NoClassDefFoundError: InputCoercionException`. Adding `com.fasterxml.jackson.core:jackson-core:2.11.2` to `pom.xml` fixed it.
- Screenshots: `maven_project_clone.png`, `maven_installed.png`, `maven_package.png`, `maven_elasticsearch_dependency.png`, `maven_repackage.png`, `maven_test.png`, `maven_jar.png`, `maven_running.png`, `maven_stopped.png`, `maven_project_closed.png`

## Task 3: Gradle Project (java-app)

- Cloned `https://gitlab.com/nanuchi/java-app.git` into `/config/IdeaProjects/java-app`.
- Set Project SDK and Gradle JVM to Temurin JDK 16, language level 8. `./gradlew --version` reported JVM 16.0.2.
- Ran `./gradlew build`, added `implementation("org.elasticsearch:elasticsearch:7.0.0")` to `build.gradle`, synced Gradle, and rebuilt.
- Found `build/libs/java-app-1.0-SNAPSHOT.jar` and ran it with `java -jar`. The app started on port 8080. Stopped it with Ctrl+C and closed the project.
- Problem and fix: the first JDK 16 download was IBM Semeru (OpenJ9), which failed to load on this kernel (`libjvm.so failed to load: j9vm29`). Replaced it with Eclipse Temurin 16 (HotSpot).
- Screenshots: `gradle_project_clone.png`, `gradle_build.png`, `gradle_elasticsearch_dependency.png`, `gradle_rebuild.png`, `gradle_jar.png`, `gradle_running.png`, `gradle_stopped.png`, `gradle_project_closed.png`

## Task 4: Node.js Project (node-project)

- Cloned `https://gitlab.com/devopsbootcamp3/node-project.git` into `/config/IdeaProjects/node-project`.
- Installed Node.js and npm, ran `npm install` inside `app`.
- `npm start` failed with `EADDRINUSE` on port 3000 because the Webtop desktop uses it. Changed `app.listen` in `app/server.js` to port 4000, and the app printed `app listening on port 4000!`.
- Opened `http://localhost:4000` in Chromium inside the container desktop and saw the project page with its profile images.
- Ran `npm test` (Jest, 1 test passed) and `npm pack`, which created `bootcamp-node-project-1.0.0.tgz`.
- Problem and fix: `sudo apt install nodejs npm` conflicted with the NodeSource `nodejs` package, so only `nodejs` was installed. npm came with it.
- Screenshots: `node_project_clone.png`, `nodejs_installed.png`, `npm_install.png`, `node_running.png`, `node_browser.png`, `npm_test.png`, `npm_pack.png`

## Task 5: React and Node.js API Bundle

- Cloned `https://github.com/bbachi/react-nodejs-example.git` into `/config/IdeaProjects/react-nodejs-example`.
- In `api`, ran `npm install` (753 packages) and checked `node_modules`.
- Built the bundle with webpack: `NODE_OPTIONS=--openssl-legacy-provider npm run build`. This created `api/server.bundle.js` (563 KiB).
- Viewed the bundle with `cat server.bundle.js | more`.
- Problem and fix: plain `npm run build` failed with `ERR_OSSL_EVP_UNSUPPORTED` because old webpack 4 does not work with Node 22 OpenSSL defaults. The legacy provider option fixed it.
- Screenshots: `react_node_project_clone.png`, `react_api_dependencies.png`, `react_api_build.png`, `react_api_bundle.png`

## Task 6: Docker Image for the Node.js Project

- Reopened `/config/IdeaProjects/node-project` and ran the commands from its root directory.
- Checked `docker --version`, listed the files with `ls` (Dockerfile is present), and listed images before the build.
- Built the image with `sudo docker build -t lab5:1.0 .`. The build copied `app`, ran `npm install` and `npm run test` successfully.
- Listed images again and found repository `lab5` with tag `1.0`.
- Screenshots: `docker_installed.png`, `dockerfile_exists.png`, `docker_images_before.png`, `docker_build.png`, `docker_images_after.png`


