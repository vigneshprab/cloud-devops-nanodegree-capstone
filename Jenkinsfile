pipeline {
    agent any
    stages {
        stage('Lint HTML & Dockerfile'){
            steps {
                sh 'tidy -q -e application/blue/*.html'
                sh 'tidy -q -e application/green/*.html'
                sh 'hadolint application/blue/Dockerfile'
                sh 'hadolint application/green/Dockerfile'
            }
        }
        stage('Build and Publish Docker Image'){
            steps{        
                script{
                    docker.withRegistry('https://registry.hub.docker.com', 'docker') {
                    def blue = docker.build("vigneshprab/blue-image","-f blue-green/blue/Dockerfile blue-green/blue")
                    def green = docker.build("vigneshprab/green-image","-f blue-green/green/Dockerfile blue-green/green")
                    blue.push()
                    green.push()    
                    }
                }
            }
        }
    }
}
