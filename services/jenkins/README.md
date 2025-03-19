# Jenkins

- Add jenkins named agent1 and fill secret in `jenkins-secret` file, Remote root directory should be `/home/jenkins/agent`.
- restart agent1: `docker compose -f services/jenkins/docker-compose.yml up -d` or `./service jenkins restart`.
