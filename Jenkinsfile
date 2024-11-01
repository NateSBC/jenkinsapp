pipeline {
    agent any
    stages {
        stage('Delete Current Images/Containers'){
            steps {
                sh 'docker rm -f $(docker ps -aq) || true'
                sh 'docker rmi -f $(docker images) || true'
            }
        }

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

        stage('UnitTest'){
            steps {
                sh '''
                python3 -m venv .venv
                . .venv/bin/activate
                pip install -r ./Task1/requirements.txt
                python3 -m unittest ./Task1/test_jenkins.py
                deactivate
            '''
            }
        }


    }
}
        
