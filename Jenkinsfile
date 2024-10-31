pipeline {
  agent any
  stages {
    stage('git scm update') {
      steps {
        git url: 'https://github.com/stone123-del/jenkinstest.git', branch: 'master'
      }
    }
    stage('delivery and deployment') {
      steps {
        sh '''
        sudo ansible master -m copy -a "src=testpod.yml dest=/root/testpod.yml" --become
        sudo docker build -t ilovesnows/keduitlab:red .
        sudo docker push ilovesnows/keduitlab:red
        '''
      }
    }
  }
}

