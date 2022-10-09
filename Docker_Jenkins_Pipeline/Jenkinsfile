pipeline {
    environment {
    registry = "SrimathiElango21/docker_automation"
    registryCredential = "dockerhub"
    dockerImage = ''
    PATH = "$PATH:/usr/local/bin"
}

    agent {
        'docker'}
    stages {
            stage('Cloning our Git') {
                steps {
                git 'https://github.com/SrimathiElango21/Setting-Up-Jenkins-Pipeline-to-Deploy-Docker-Swarm'
                }
            }

            stage('Building Docker Image') {
                steps {
                    script {
                        dockerImage = docker.build registry + ":$BUILD_NUMBER"
                    }
                }
            }

            stage('Deploying Docker Image to Dockerhub') {
                steps {
                    script {
                        docker.withRegistry('', registryCredential) {
                        dockerImage.push()
                        }
                    }
                }
            }

            stage('Cleaning Up') {
                steps{
                  sh "docker rmi $registry:$BUILD_NUMBER"
                }
            }
        }
    }