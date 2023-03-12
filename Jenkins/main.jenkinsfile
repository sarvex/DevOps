pipeline {
  agent any
  stages {
    stage('Checking out the repo') {
      steps {
        git(branch: 'jenkins', url: 'https://github.com/pradumnasaraf/DevOps')
      }
    }
    stage('Building the image') {
      when{
        expression { BRANCH_NAME == 'jenkins' }
      }
      steps {
        sh 'docker build -t sarafpradumna/devops:latest .'
      }
    }
  
    stage('docker login') {
      steps {
        withCredentials([usernamePassword(credentialsId: 'DOCKERHUB_CREDENTIALS', passwordVariable: 'DOCKERHUB_PASSWORD', usernameVariable: 'DOCKERHUB_USERNAME')]) {
          sh 'echo $DOCKERHUB_PASSWORD | docker login --username $DOCKERHUB_USERNAME --password-stdin'
        }
      }
    }

    stage('Pushing the image') {
      steps {
        sh 'docker push sarafpradumna/devops:latest'
      }
    }

    stage("docker logout") {
      steps {
        sh 'docker logout'
      }
    }
  }
  
}