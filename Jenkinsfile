pipeline {

  environment {
    dockerimagename = "magdy79/boots"
    dockerImage = ""
  }

  agent any

  stages {

    stage('Checkout Source') {
      steps {
        git 'https://github.com/matriix00/simple-bootstrap.git'
      }
    }

    stage('Build image') {
      steps{
        script {
          dockerImage = docker.build('magdy79/boots')
        }
      }
    }

    stage('Pushing Image') {
      environment {
               registryCredential = 'dockerhub-secret'
           }
      steps{
        script {

          docker.withRegistry( 'https://registry.hub.docker.com', registryCredential ) {
            dockerImage.push("latest")
          }
        }
      }
    }
      stage('Deploying App to Kubernetes') {
         steps{
          script {
             //  sh """
            //   kubectl apply -f deploymentservice.yaml
             //  echo done
            //"""
             kubernetesDeploy(configs: "deploymentservice.yaml", kubeconfigId: "kubernetes")
          }
         }
          
      
      
    }

  }

}
