pipeline {
    agent any
    stages {
        stage('Delete Current Images/Containers'){
            steps {
                sh 'docker rm -f $(docker ps -aq) || true'
                sh 'docker rmi -f $(docker images) || true'
            }
        }
        stage('Build Image'){
            steps {
                sh 'docker build -t flask Task1'

            }       
        }
        stage('Run Container'){
            steps {
                sh 'docker run -d -p 80:5500 --name flask flask'

            }       
        }
        stage('Trivy'){
            steps {
                sh 'trivy image flask'
                sh 'trivy image -f json -o results.json flask'
            }
        }
    
    }
}
