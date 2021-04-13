pipeline {
  environment {
    imagename = "kibr1371/lesson2"
    registryCredential = 'dockerhub_id'
    dockerImage = ''
  }
  agent any
  stages {
    stage('Cloning Git') {
      steps {
        git([url: 'https://kibr1371@github.com/kibr1371/devops.git', branch: 'master'])
      }
    }
    stage('Building image') {
      steps{
        script {
          dockerImage = docker.build imagename
        }
      }
    }
    stage('Deploy Image') {
      steps{
        script {
          docker.withRegistry( '', registryCredential ) {
            dockerImage.push("$BUILD_NUMBER")
              dockerImage.push('latest')
          }
        }
      }
    }
    stage('Run Docker image') {
      steps{
        sh "docker run -p8585:9090 -d $imagename:latest"
        
      }
    }
  }
}