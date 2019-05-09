pipeline {
  agent {
    docker {
      image 'eed3si9n/sbt:jdk8-alpine'
    }
  }
  stages {
    stage('Build') {
      steps {
        sh 'sbt -sbt-dir /localhome/jenkinssbt/workspace/sbt-integration/.sbt about'
      }
    }
  }
}
