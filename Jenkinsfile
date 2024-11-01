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
                sh 'trivy image --severity HIGH,CRITICAL flask'
                sh 'trivy image -f json -o results.json flask'
            }
        }

        stage ('UnitTest'){
            steps {
                sh '''
                python3 -m venv .venv
                . .venv/bin/activate
                pip install -r ./Task1/requirements.txt
                python3 -m unittest discover -s /Task1/tests .
                deactivate
            '''
            }
        }

        stage('Archive Artifact'){
            steps {
                archiveArtifacts artifacts: 'results.json', followSymlinks: false
            }
        }
    }
}
