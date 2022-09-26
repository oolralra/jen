pipeline {
  agent any
  stages {
    stage('git scm update') {
      steps {
        git url: 'https://github.com/oolralra/jen', branch: 'main'
      }
    }
    stage('docker build and push') {
      steps {
        sh '''
        sudo docker build -t oolralra/myweb:1.3 .
        sudo docker login -u $DOCKER_ID -p $DOCKER_PASS --password-stdin
        sudo docker push oolralra/myweb:1.3

        '''
      }
    }
    stage('deploy k8s') {
      steps {
        sh '''
        sudo kubectl apply -f deploy.yml
        '''
      }
    }
  }
}
