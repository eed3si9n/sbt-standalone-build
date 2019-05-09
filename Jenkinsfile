pipeline {
  agent {
    docker {
      image 'eed3si9n/sbt:jdk8-alpine'
      args '-w /opt/workspace'
    }
  }
  stages {
    stage('Test') {
      steps {
        sh 'mkdir -p /root'
        sh 'export HOME=/root'
        sh 'env'
        sh 'sbt about'
      }
    }
  }
}
