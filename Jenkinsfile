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
        sh '''kubectl apply -f master-deployment.yaml
              kubectl rollout restart deployment second-app-deployment
        '''
    }
    }
  }
}
