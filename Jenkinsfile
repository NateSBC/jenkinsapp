pipeline {
    agent any
    stages {
        stage('First Stages'){
            steps {
                sh 'docker rm -f $(docker ps -aq) || true'
                sh 'docker rmi -f $(docker images) || true'
            }
        }
        stage('Second Stage'){
            steps {
                sh 'docker build -t flask Task1'

            }       
        }
        stage('Third Stage'){
            steps {
                sh 'docker run -d -p 80:5500 --name flask flask'

            }       
        }
    }
}
