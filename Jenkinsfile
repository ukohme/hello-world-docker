pipeline {
  environment {
    registry = "datrotech/docker-java-datroapp"
    registryCredential = 'DockerHub_credentials'
    dockerImage = ''
  }
  agent any
  stages {
    stage('get scm') {
      steps {
	  git branch: 'main', credentialsId: 'githun_credentials', url: 'https://github.com/ukohme/hello-world-docker.git'
       }
    }
    stage('Building image') {
      steps{
        script {
          dockerImage = docker.build registry + ":v$BUILD_NUMBER"
        }
      }
    }
    stage('push image') {
      steps{
        script {
          docker.withRegistry( '', registryCredential ) {
            dockerImage.push()
          }
        }
      }
    }
    stage('Remove old docker image') {
      steps{
        sh "docker rmi $registry:v$BUILD_NUMBER"
      }
    }
  }
}
