pipeline {
    agent any
    stages {
        stage('Lint HTML & Dockerfile'){
            steps {
                sh 'tidy -q -e application/blue/*.html'
                sh 'tidy -q -e application/green/*.html'                
            }
        }
		
        stage('Build and Publish Docker Image'){
            steps{        
                script{
                    docker.withRegistry('https://registry.hub.docker.com', 'docker') {
                    def blue = docker.build("vigneshprab/blue-image","-f application/blue/Dockerfile application/blue")
                    def green = docker.build("vigneshprab/green-image","-f application/green/Dockerfile application/green")
                    blue.push()
                    green.push()    
                    }
                }
            }
        }
    }
}
