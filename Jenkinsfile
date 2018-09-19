pipeline {
  agent any
  stages {
    stage('build') {
      steps {
        sh 'docker build -t registry.cn-hangzhou.aliyuncs.com/yanmei/kube-app:$BUILD_NUMBER .'
      }
    }
  }
}
