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

      }
    }

    stage('Build with Maven') {
      steps {
        sh 'mvn package'
      }
    }

    stage('Run JAR file') {
      steps {
        sh 'java -jar target/*.jar'
      }
    }

  }
}