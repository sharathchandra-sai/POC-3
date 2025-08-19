pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/sharathchandra-sai/POC-3.git'
            }
        }
        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }
        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }
        stage('Docker Build') {
            steps {
                sh 'docker build -t poc3-app .'
            }
        }
        stage('Docker Build & Push') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'docker-hub-creds', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
                    sh 'echo $DOCKER_PASS | docker login -u $DOCKER_USER --password-stdin'
                    sh 'docker build -t sharathkodati/sharathproject-1 .'
                    sh 'docker push sharathkodati/sharathproject-1'
                }
            }
        }
    }
}
