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
        withDockerRegistry(credentialsId: 'dockerhub', url: 'https://registry.cn-hangzhou.aliyuncs.com') {
          sh 'docker push registry.cn-hangzhou.aliyuncs.com/yanmei/kube-app:$BUILD_NUMBER'
        }

      }
    }
    stage('push chart') {
      steps {
        script {
          def filename = 'helm/kube-app/values.yaml'
          def data = readYaml file: filename
          data.image.tag = env.BUILD_NUMBER
          sh "rm $filename"
          writeYaml file: filename, data: data
        }

        script {
          def filename = 'helm/kube-app/Chart.yaml'
          def data = readYaml file: filename
          data.version = env.BUILD_NUMBER
          sh "rm $filename"
          writeYaml file: filename, data: data
        }

        sh 'helm push helm/kube-app https://repomanage.rdc.aliyun.com/helm_repositories/24409-yanmei --username=GeLbkQ --password=fm3MqELmc8 --version=$BUILD_NUMBER'
      }
    }
  }
}