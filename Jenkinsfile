pipeline {
  agent any
  stages {
    stage('Log Tool Version') {
      parallel {
        stage('Log Tool Version') {
          steps {
            sh '''mvn --version
git --version
java -version'''
          }
        }

        stage('Check for POM') {
          steps {
            fileExists 'pom.xml'
          }
        }

        stage('SonarQube analysis') {
          steps {
            withSonarQubeEnv("${SONARSERVER}") {
              sh 'mvn package sonar:sonar'
            }

          }
        }

      }
    }

    stage('Run JAR file') {
      steps {
        sh 'JENKINS_NODE_COOKIE=dontKillMe nohup java -jar target/*.jar --server.port=8083 &'
      }
    }

  }
  environment {
    SONARSERVER = 'sonarserver'
  }
}