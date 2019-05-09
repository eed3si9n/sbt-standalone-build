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
        sh 'cd /localhome/jenkinssbt/workspace/sbt-integration/ && mkdir target/'
        sh 'git clone -n -q https://github.com/sbt/io.git target/io'
      }
    }
  }
}
