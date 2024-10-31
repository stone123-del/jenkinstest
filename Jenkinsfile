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
        sudo docker build -t ilovesnows/keduitlab:red .
        sudo docker push ilovesnows/keduitlab:red
        sudo ansible node -m shell -a "sudo docker pull ilovesnows/keduitlab:red"
        sudo ansible master -m shell -a "sudo kubectl create deploy jihojjang --replicas=3 --port=80 --image=ilovesnows/keduitlab:red"
        sudo ansible master -m shell -a "sudo kubectl expose deploy jihojjang --type=LoadBalancer --port=80 --target-port=80 --name=jihojjang"

        
        '''
      }
    }
  }
}

