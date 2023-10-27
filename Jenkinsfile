
pipeline {
  agent any
  environment {
    DOCKERHUB_CREDENTIALS = credentials('DOCKER_HUB_CREDS')
  }
  stages {
    stage('Build') {
      steps {
	    sh 'docker build -t sailusha/jenkins-repos:$BUILD_NUMBER .'
      }
    }
    stage('Login') {
      steps {
         sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
      }
    }
    stage('Push') {
      steps {
         sh 'docker push sailusha/jenkins-repos:$BUILD_NUMBER'
      }
    }
    
  }
  post {
    always {
       sh 'docker logout'
    }
  }
}
