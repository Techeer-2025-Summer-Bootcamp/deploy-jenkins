pipeline {
    agent any

    environment {
        DEPLOY_SERVER = 'whysano517@34.56.8.252'
        DOCKER_COMPOSE_FILE = 'docker-compose.yml'
    }

    stages {
        stage('SSH into server') {
            steps {
                sshagent(['service-ssh']) {
                        sh """
                        scp -o StrictHostKeyChecking=no ${DOCKER_COMPOSE_FILE} ${DEPLOY_SERVER}:/home/whysano517/
                        ssh -o StrictHostKeyChecking=no ${DEPLOY_SERVER} '
                        cd ~ &&
                        ls -al &&
                        docker compose -f ${DOCKER_COMPOSE_FILE} down --remove-orphans
                        docker compose -f ${DOCKER_COMPOSE_FILE} pull &&
                        docker compose -f ${DOCKER_COMPOSE_FILE} up -d'
                        """
                    }
            }
        }
    }
}