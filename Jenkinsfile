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
              containerPort: 80
        '''
    }
  }
  stages {
    stage('Run nginx') {
      steps {
        container('nginx-cont') {
          sh 'echo hiiiii'
        }
      }
    }
  }
}
