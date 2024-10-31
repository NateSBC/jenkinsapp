pipeline {
    agent any
    stages {
        stage('First Stages'){
            steps {
                sh 'sudo docker rm -f $(docker ps -aq)'
                sh 'docker rmi -f $(docker images)'
            }
        }
        
    }
}
