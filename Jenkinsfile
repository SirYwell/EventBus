pipeline {
  agent any
  stages {
    stage('fetch') {
      steps {
        git(url: 'https://github.com/cpw/eventbus.git', changelog: true)
      }
    }
    stage('buildandtest') {
      steps {
        sh './gradlew cleanTest test'
        junit 'build/test-results/test/*.xml'
      }
    }
    stage('publish') {
      environment {
        FORGE_MAVEN = 'credentials(\'forge-maven-forge-user\')'
      }
      steps {
        sh './gradlew publish -PforgeMavenUser=${FORGE_MAVEN_USR} -PforgeMavenPassword=${FORGE_MAVEN_PSW}'
      }
    }
  }
}