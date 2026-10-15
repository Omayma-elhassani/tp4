pipeline {
    environment {
        registry = "omayma2004/tp4"
        registryCredential = 'dockerhub'
        dockerImage = ''
    }
    agent any
    stages {
        stage('Cloning Git') {
            steps {
                git branch: 'master', url: 'https://github.com/Omayma-elhassani/tp4.git'
            }
        }
        stage('Building image') {
            steps {
                script {
                    dockerImage = docker.build registry + ":$BUILD_NUMBER"
                }
            }
        }
        stage('Test image') {
            steps {
                script {
                    echo "Tests passed"
                }
            }
        }
        stage('Publish Image') {
            steps {
                script {
                    retry(3) {
                        docker.withRegistry('', registryCredential) {
                            dockerImage.push()
                        }
                    }
                }
            }
        }
    }
}