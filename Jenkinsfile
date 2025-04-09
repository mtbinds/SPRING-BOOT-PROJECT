pipeline {

  agent any

  tools {
    maven 'Maven' // Assure-toi que ce nom correspond bien à l'installation Maven dans Jenkins
  }

  environment {
    dockerimagename = "spring-boot-k8s"
  }

  stages {

    stage('Build App') {
      steps {
        sh 'mvn clean package -DskipTests'
      }
    }

/*
    stage('Build Docker Image') {
      steps {
        script {
          dockerImage = docker.build("${env.dockerimagename}:latest")
        }
      }
    }
*/
    stage('Deploy to Kubernetes') {
      steps {
        script {
          sh 'kubectl apply -f deployment-k8s.yaml'
        }
      }
    }

  }

  post {
    success {
      echo 'Déploiement réussi sur le cluster Docker Desktop Kubernetes !'
    }
    failure {
      echo 'Le déploiement a échoué.'
    }
  }
}
