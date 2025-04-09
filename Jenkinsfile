pipeline {
    agent any

    triggers {
        pollSCM('*/1 * * * *') // Vérifie le SCM toutes les minutes
    }

    options {
        buildDiscarder(logRotator(numToKeepStr: '5'))
    }

    environment {
        DOCKER_IMAGE_NAME = 'madjidtaoualit/myapi' // remplace avec ton nom d'utilisateur Docker Hub
        IMAGE_TAG = 'latest'
    }

    stages {
        stage('Build Docker Image') {
            steps {
                dir('MyApi') {
                    sh 'docker build -t $DOCKER_IMAGE_NAME:$IMAGE_TAG .'
                }
            }
        }

        stage('Push Docker Image') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub_credentials', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
                    sh '''
                        echo "$DOCKER_PASS" | docker login -u "$DOCKER_USER" --password-stdin
                        docker push $DOCKER_IMAGE_NAME:$IMAGE_TAG
                        docker logout
                    '''
                }
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                sh '''
                    microk8s kubectl apply -f deployment.yaml
                    microk8s kubectl apply -f service.yaml
                '''
            }
        }
    }
}
