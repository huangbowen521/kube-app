pipeline {
  agent any
  stages {
    stage('build') {
      steps {
        sh 'docker build -t registry.cn-hangzhou.aliyuncs.com/yanmei/kube-app:$BUILD_NUMBER .'
      }
    }
    
    stage('push image') {
    steps {
        withDockerRegistry([credentialsId: 'dockerhub', url: 'https://registry.cn-hangzhou.aliyuncs.com']) {
            //修改为自己的镜像
            sh 'docker push registry.cn-hangzhou.aliyuncs.com/yanmei/kube-app:$BUILD_NUMBER'
        }
    }
}
  }
}
