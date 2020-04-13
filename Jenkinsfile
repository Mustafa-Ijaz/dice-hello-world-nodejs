pipeline {
  agent any
  environment {
    registryCredential = 'dockerhub'
   }
  stages {
    stage('Build') {
      steps {
          sh 'docker build -t mustafa75/test-image .'
      }
     }
    stage('Test') {
      steps {
          sh 'docker container run -p 8001:8080 --name node -d mustafa75/test-image'
          sh 'curl -I http://localhost:8001'
      }
    }
    stage('Publish') {
      steps{
        script {
        docker.withRegistry( '', registryCredential ) {
        sh 'docker push mustafa75/test-image:latest'
          }
        }
      }
    }
  }
}
