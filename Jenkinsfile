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
        docker build -t imsnghyun/cicdtest:blue .
        docker push imsnghyun/cicdtest:blue
        ''' 
      }
    }
    stage('deploy kubernetes') {
      steps {
        sh '''
        kubectl create deploy myweb1 --image=imsnghyun/cicdtest:blue
        kubectl expose deploy myweb1 --type="LoadBalancer" --port=80 --target-port=80 --protocol="TCP"
        
        '''
      }
    }
  }
}
