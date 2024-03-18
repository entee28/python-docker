pipeline {
    agent none

    stages {
        stage('Build Docker Image with DinD') {
            agent {
                kubernetes {
                    defaultContainer 'dind'
                    yamlFile 'dind.yaml'
                }
            }

            environment {
                ACR_CREDS = credentials('acr-sp')
            }

            steps {
                sh 'echo $ACR_CREDS_PSW >> ./password.txt'
                sh 'cat ./password.txt | docker login thachthucregistry.azurecr.io --username $ACR_CREDS_USR --password-stdin'
                sh 'docker build -t thachthucregistry.azurecr.io/minimal-python:latest .'
                sh 'docker push thachthucregistry.azurecr.io/minimal-python:latest'
            }
        }
    }
}
