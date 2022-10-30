// pipeline {
//   agent {
//     kubernetes {
//       yaml '''
//         apiVersion: v1
//         kind: Pod
//         spec:
//           containers:
//           - name: nginx-cont
//             image: nginx
//             ports:
//              - containerPort: 80
//         '''
//     }
//   }
//   stages {
//     stage('build') {
//             steps {
//                 echo 'Starting to build docker image'
//                 sh " docker build . -t bootstrap-web-app:${env.BUILD_NUMBER}"
//                 echo "Build Image Compeletd"
//                 sh " docker tag bootstrap-web-app:${env.BUILD_NUMBER} magdy79/bootstrap-web-app:${env.BUILD_NUMBER}"
                
//             }
//         }
//     stage('Run nginx') {
//       steps {
//         container('nginx-cont') {
//           sh 'echo hiiiii'
//         }
//       }
//     }
//   }
// }

// pipeline {
//     agent { dockerfile true }
//     stages {
//          stage('Run nginx') {
//              steps {
//              sh 'echo hiiiii'
//         }
//          }
//     }
// }

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
      steps {
        script {
          kubernetesDeploy(configs: "deploymentservice.yml", kubeconfigId: "jenkins-master")
        }
      }
    }

  }

}