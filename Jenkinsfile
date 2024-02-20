pipeline {
  agent any
  stages {
    stages('git scm update') {
      steps {
        git url: 'https://github.com/imsnghn/cicdtest.git', branch: 'main'
      }
    }
    stage('docker build and push') {
      steps {
        sh '''
        sudo docker build -t imsnghyun/cicdtest:blue .
        sudo docker push imsnghyun/cicdtest:blue
        ''' 
      }
    }
    stage('deploy and service') {
      steps {
        sh '''
        ansible master -m command -a 'kubectl create deploy web-green --replicas=3 --image=imsnghyun/cicdtest:blue'
        ansible master -m command -a 'kubectl expose deploy web-green --type=LoadBalancer --port=80 --target-port=80 --name=web-green-svc'
        '''
      }
    }
  }
}
