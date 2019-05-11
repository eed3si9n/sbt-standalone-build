pipeline {
  agent {
    docker {
      image 'eed3si9n/sbt:jdk8-alpine'
    }
  }

  environment {
    DATETIME_TAG = java.time.LocalDateTime.now().format(java.time.format.DateTimeFormatter.ofPattern("yyyyMMdd'T'HHmmss"))
    BUILD_VERSION = "1.3.0-bin-" + "$DATETIME_TAG"
  }

  stages {
    stage('Build') {
      steps {
        echo "timestamp ${DATETIME_TAG}"

        sh 'cd /localhome/jenkinssbt/workspace/sbt-integration/'
        sh 'rm -rf target && mkdir -p target'
        sh 'rm -rf .sbt && cp -r /home/demiourgos1/.sbt .sbt'
        sh 'rm -rf .sbt/preloaded/org.scala-lang/'
        sh 'rm -rf .sbt/preloaded/org.scala-lang.modules/'
        sh 'git clone -n -q https://github.com/sbt/io.git target/io'
        dir('target/io') {
          sh "git fetch -f -u -q origin '+refs/pull/*/head:refs/pull/*/head' '+refs/tags/*:refs/tags/*' '+refs/heads/*:refs/heads/*'"
          sh 'git clean -fdxq'
          sh 'git reset -q --hard "${io}"'
          sh "sbt -Dsbt.build.version=${BUILD_VERSION} -sbt-dir /localhome/jenkinssbt/workspace/sbt-integration/.sbt -ivy /localhome/jenkinssbt/workspace/sbt-integration/.ivy -no-colors publishLocal"
        }

        sh 'git clone -n -q https://github.com/sbt/util.git target/util'
        dir('target/util') {
          sh "git fetch -f -u -q origin '+refs/pull/*/head:refs/pull/*/head' '+refs/tags/*:refs/tags/*' '+refs/heads/*:refs/heads/*'"
          sh 'git clean -fdxq'
          sh 'git reset -q --hard "${util}"'
          sh 'sbt -sbt-dir /localhome/jenkinssbt/workspace/sbt-integration/.sbt -ivy /localhome/jenkinssbt/workspace/sbt-integration/.ivy -no-colors publishLocal'
        }

        sh 'git clone -n -q https://github.com/sbt/librarymanagement.git target/librarymanagement'
        dir('target/librarymanagement') {
          sh "git fetch -f -u -q origin '+refs/pull/*/head:refs/pull/*/head' '+refs/tags/*:refs/tags/*' '+refs/heads/*:refs/heads/*'"
          sh 'git clean -fdxq'
          sh 'git reset -q --hard "${librarymanagement}"'
          sh 'sbt -sbt-dir /localhome/jenkinssbt/workspace/sbt-integration/.sbt -ivy /localhome/jenkinssbt/workspace/sbt-integration/.ivy -no-colors publishLocal'
        }

        sh 'git clone -n -q https://github.com/sbt/zinc.git target/zinc'
        dir('target/zinc') {
          sh "git fetch -f -u -q origin '+refs/pull/*/head:refs/pull/*/head' '+refs/tags/*:refs/tags/*' '+refs/heads/*:refs/heads/*'"
          sh 'git clean -fdxq'
          sh 'git reset -q --hard "${zinc}"'
          sh 'sbt -sbt-dir /localhome/jenkinssbt/workspace/sbt-integration/.sbt -ivy /localhome/jenkinssbt/workspace/sbt-integration/.ivy -no-colors publishLocal'
        }

        sh 'git clone -n -q https://github.com/sbt/sbt.git target/sbt'
        dir('target/sbt') {
          sh "git fetch -f -u -q origin '+refs/pull/*/head:refs/pull/*/head' '+refs/tags/*:refs/tags/*' '+refs/heads/*:refs/heads/*'"
          sh 'git clean -fdxq'
          sh 'git reset -q --hard "${sbt}"'
          sh 'sbt -sbt-dir /localhome/jenkinssbt/workspace/sbt-integration/.sbt -ivy /localhome/jenkinssbt/workspace/sbt-integration/.ivy -no-colors publishLocal'
        }
      }
    }
  }
}
