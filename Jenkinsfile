pipeline {
    agent any
    stages {
        stage('Delete Current Images/Containers'){
            steps {
                sh 'docker rm -f $(docker ps -aq) || true'
                sh 'docker rmi -f $(docker images) || true'
            }
        }

        stage('Second Stage'){

        stage('Create Network') {

            steps {
                sh 'docker network create new-network || true'
            }
        }        

        stage('Build Image'){
            steps {
                sh 'docker build -t flask Task1'
                sh 'docker build -t mynginx -f ./Task1/Dockerfile.nginx .'

            }       
        }

        stage('Third Stage'){
            steps {
                sh 'docker run -d -p 80:80 --name flask flask'


        stage('Scan'){
            steps {
                sh 'trivy image -f json -o results.json flask'
            }
        }
         stage('Archive Artifact'){
            steps {
                archiveArtifacts artifacts: 'results.json', followSymlinks: false
            }
        }
        stage('Run Container'){
            steps {
                sh 'docker run -d --name flask --network new-network flask:latest'
                sh 'docker run -d -p 80:80 --name mynginx --network new-network mynginx'
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



        stage ('UnitTest'){
            steps {
                sh '''
                python3 -m venv .venv
                . .venv/bin/activate
                pip install -r ./Task1/requirements.txt
                python3 -m unittest discover -s .
                deactivate
            '''
            }
        }


    }
}
