pipeline {
    agent any

    stages {

        stage('Clone Code') {
            steps {
                git url: 'https://github.com/Soumi-Pandit12/quicknotes-flask-mysql-docker.git', branch: 'main'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t quicknotes-app .'
            }
        }

        stage('Remove Old Container') {
            steps {
                sh 'docker rm -f quicknotes-container || true'
            }
        }

        stage('Run Container') {
            steps {
                sh 'docker run -d -p 5000:5000 --name quicknotes-container quicknotes-app'
            }
        }
    }
}
