pipeline {
  agent {
    kubernetes {
      yaml '''
        apiVersion: v1
        kind: Pod
        spec:
          containers:
          - name: nginx-cont
            image: nginx
            ports:
             - containerPort: 80
        '''
    }
  }
  stages {
    stage('build') {
            steps {
                echo 'Starting to build docker image'
                // sh " docker build . -t bootstrap-web-app:${env.BUILD_NUMBER}"
                // echo "Build Image Compeletd"
                // sh " docker tag bootstrap-web-app:${env.BUILD_NUMBER} magdy79/bootstrap-web-app:${env.BUILD_NUMBER}"
                
            }
        }
    stage('Run nginx') {
      steps {
        container('nginx-cont') {
          sh 'echo hiiiii'
        }
      }
    }
  }
}
