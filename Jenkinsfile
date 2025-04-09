pipeline {

  agent any

  tools {
    // Nom de l'installation Maven définie dans Jenkins
    maven 'Maven'
  }

  environment {
    dockerimagename = "spring-boot-k8s"
    dockerImage = ""
  }

  stages {

    stage('Build App') {
      steps {
        sh 'mvn clean package'
      }
    }

    stage('Build Docker Image') {
      steps {
        script {
          dockerImage = docker.build("${dockerimagename}:latest")
        }
      }
    }

    stage('Deploy to Kubernetes') {
      steps {
        script {
          // Vérifie que kubectl pointe vers le bon cluster
          sh 'kubectl config use-context docker-desktop'
          // Applique les ressources Kubernetes
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
