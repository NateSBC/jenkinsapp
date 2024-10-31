pipeline {
    agent any
    stages {
        stage('First Stages'){
            steps {
                sh 'docker rm -f $(docker ps -aq)'
                sh 'docker rmi -f $(docker images)'
            }
        }
        stage('Second Stage'){
            steps {
                sh 'docker build -t flask Task1'

            }       
        }