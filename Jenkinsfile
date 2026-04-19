pipeline {
    agent any

    options {
        timeout(time: 10, unit: 'MINUTES')
    }

    stages {

        stage("code clone") {
            steps {
                deleteDir()
                git url: "https://github.com/Soumi-Pandit12/quicknotes-flask-mysql-docker.git", branch: "main"
            }
        }

        stage("build") {
            steps {
                sh "docker build -t quicknotes-flask-mysql-docker ."
            }
        }

        stage("Push to Docker Hub") {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: "dockerHubCreds",
                    usernameVariable: "dockerHubUser",
                    passwordVariable: "dockerHubPass"
                )]) {
                    sh '''
                    echo $dockerHubPass | docker login -u $dockerHubUser --password-stdin

                    docker tag quicknotes-flask-mysql-docker $dockerHubUser/quicknotes-flask-mysql-docker:latest
                    docker push $dockerHubUser/quicknotes-flask-mysql-docker:latest
                    '''
                }
            }
        }

        stage("deploy") {
            steps {
                sh '''
                cp .env.example .env

                docker compose down || true

                docker pull soumipandit/quicknotes-flask-mysql-docker:latest

                docker compose up -d --force-recreate
                '''
            }
        }
    }
}
