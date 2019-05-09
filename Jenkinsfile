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
        dir('target/io') {
          sh "git fetch -f -u -q origin '+refs/pull/*/head:refs/pull/*/head' '+refs/tags/*:refs/tags/*' '+refs/heads/*:refs/heads/*'"
          sh 'git clean -fdxq'
          sh 'git reset -q --hard "${io}"'
          sh 'sbt -sbt-dir /localhome/jenkinssbt/workspace/sbt-integration/.sbt -no-colors test'
        }
      }
    }
  }
}
