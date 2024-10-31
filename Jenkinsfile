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
        ansible node -m shell -a "sudo docker pull ilovesnows/keduitlab:${now}"
        ansible master -m shell -a "sudo kubectl create deploy web-${now} --replicas=3 --port=80 --image=ilovesnows/keduitlab:${now}"
        ansible master -m shell -a "sudo kubectl expose deploy web-${now} --type=LoadBalancer --port=80 --target-port=80 --name=web-${now}-svc"
        '''
      }
    }
    stage('deploy and service') {
      steps{
        sh '''
        sudo kubectl apply -f testpod.yml
        '''
      }
    }
  }
}

