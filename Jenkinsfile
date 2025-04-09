pipeline {
  agent any
  triggers {
    pollSCM('*/1 * * * *')
  }
  options {
    buildDiscarder logRotator(artifactDaysToKeepStr: '', artifactNumToKeepStr: '5', daysToKeepStr: '', numToKeepStr: '5')
  }

  stages {
    /*
    stage('Clone and Checkout') {
      steps {
        git 'https://github.com/mtbinds/SPRING-BOOT-PROJECT.git'
      }
    }
    */
    stage('Compile') {
      steps {
        sh "mvn clean compile"
      }
    }
    stage('Test') {
      steps {
        sh "mvn test"
      }
    }
    stage('Package') {
      steps {
        sh "mvn package"
      }
    }
    stage('Install') {
      steps {
        sh "mvn install"
      }
    }
    stage('build docker image') {
      steps {
        sh 'docker build -t amitchavda00/spring-crud-jenkins-pipeline:latest .'
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
        sh 'kubectl apply -f user-api-service.yaml'
      }
    }
  }
}