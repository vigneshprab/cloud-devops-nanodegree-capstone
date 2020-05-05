pipeline {
    agent any
    stages {
        stage('Lint HTML'){
            steps {
                sh 'tidy -q -e application/blue/*.html'
                sh 'tidy -q -e application/green/*.html'                
            }
        }
		stage('Lint Dockerfile') {
            steps {
                script {
                    dir('app') {
                            docker.image('hadolint/hadolint:latest-debian').inside() {
                                sh 'hadolint ./Dockerfile | tee -a hadolint_lint.txt'
                                sh '''
                                    lintErrors=$(stat --printf="%s"  hadolint_lint.txt)
                                    if [ "$lintErrors" -gt "0" ]; then
                                        echo "Errors have been found, please see below"
                                        cat hadolint_lint.txt
                                    exit 1
                                    else
                                        echo "There are no erros found on Dockerfile!!"
                                    fi
                                '''
                            }
                        }
                }
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
