pipeline {
    agent any

    stages {

        
        stage('Clone Success') {
            steps {
                echo 'Git clone successful!'
            }
        }
        
        stage('Debug PATH') {
          steps {
            sh 'echo $PATH'
            sh 'which docker || true'
          }
        }
        
        stage('Build Docker Image') {
            steps {
                sh 'docker build -t mywebsite:latest .'
            }
        }

        stage('Stop Old Container') {
            steps {
                sh 'docker stop mywebsite || true'
                sh 'docker rm mywebsite || true'
            }
        }

        stage('Run New Container') {
            steps {
                sh '''
                docker run -d \
                  -p 8081:80 \
                  --name mywebsite \
                  mywebsite:latest
                '''
            }
        }

    }
}
