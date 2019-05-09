pipeline {
  agent {
    docker {
      image 'eed3si9n/sbt:jdk8-alpine'
    }
  }
  stages {
    stage('Build') {
      steps {
        sh 'cd /localhome/jenkinssbt/workspace/sbt-integration/'
        sh 'rm -rf target && mkdir -p target'
        sh 'git clone -n -q https://github.com/sbt/io.git target/io'
        sh 'cd target/io'
        sh 'sbt -sbt-dir /localhome/jenkinssbt/workspace/sbt-integration/.sbt -no-colors test'
      }
    }
  }
}
