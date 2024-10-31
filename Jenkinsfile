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
        ansible master -m copy -a "src=testpod.yml dest=/root/testpod.yml" --become
        now=$(date +%y%m%d%H%M)
        sudo docker build -t ilovesnows/keduitlab:${now} .
        sudo docker push ilovesnows/keduitlab:${now}
        '''
      }
    }
  }
}

