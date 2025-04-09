pipeline {
  
  agent {
        label ‘main-host’
  }

  stages {
    /*
    stage('Clone and Checkout') {
      steps {
        git 'https://github.com/mtbinds/SPRING-BOOT-PROJECT.git'
      }
    }
    */

    stage('build docker image') {
      steps {
        sh '''cd MyApi
        docker build -t myapi:latest .'''
      }
    }

    /*
    stage('push docker image') {
      steps {
        script {
          //withCredentials([string(credentialsId: 'dockerhub_token', variable: 'dockerhub_token')]) {
          //sh 'docker login -u amitchavda00 -p ${dockerhub_token}'
          sh 'docker push amitchavda00/spring-crud-jenkins-pipeline:latest'
          //}
        }
      }
    }
    */

    stage('deploy in kubernetes') {
      steps {
        sh '''kubectl apply -f deployment.yaml
            kubectl apply -f service.yaml'''
      }
    }
  }
}