pipeline {
  agent {
    docker {
      image 'eed3si9n/sbt:jdk8-alpine'
    }
  }
  stages {
    stage('Test') {
      steps {
        sh 'env'
        sh 'sbt -sbt-dir /localhome/jenkinssbt/workspace/sbt-integration/.sbt about'
      }
    }
  }
}
