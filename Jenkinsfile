pipeline {
  agent any
  stages{
    stage('Checkout code'){
      steps{
        checkout scm
    }
    }
    /*
    stage('build'){
      steps{
        sh '''docker build -t react .'''
      }
    }
    */

    /*
    stage('Push image'){
          steps{
            sh '''docker tag react <imagename>
            docker push <imagename>'''
      }
    }
    */
    stage('Deploy'){
      steps{
        sh '''kubectl apply -f /templates/deployment.yaml
        kubectl apply -f /templates/service.yaml
        '''
    }
    }
  }
}
