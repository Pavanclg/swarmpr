pipeline {
    agent any

    tools {
        maven 'Maven3'
    }

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Docker Build') {
            steps {
                sh 'docker build -t swarm:latest .'
            }
        }

        stage('Docker Push') {
            steps {
                sh '''
                docker tag swarm:latest pavanwork10/swarm:latest
                docker push pavanwork10/swarm:latest
                '''
            }
        }

        stage('Deploy to Docker Swarm') {
            steps {
                sh '''
                docker service rm swarm-service || true
                docker service create --name swarm-service pavanwork10/swarm:latest
                '''
            }
        }
    }
}