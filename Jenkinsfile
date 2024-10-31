pipeline {
  agent any
  stages {
    stage('git scm update') {
      steps {
        git url: 'https://github.com/stone123-del/jenkinstest.git', branch: 'main'
      }
    }
    stage('docker build and push') { 
      steps {
        sh '''
        sudo docker build -t ilovesnows/keduit:puple .
        sudo docker push ilovesnows/keduit:puple
        '''
      }
    }
    stage('deploy and service') {
      steps {
        sh '''
        sudo kubectl apply -f test.yml
        '''
      }
    }
  }
}
