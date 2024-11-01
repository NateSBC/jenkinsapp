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
        stage('Third Stage'){
            steps {
                sh 'docker run -d 80:80 --name flask flask'

            }       
        }
    }
}
