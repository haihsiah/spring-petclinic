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

    stage('Build Jar') {
      steps {
        sh 'mvn package'
      }
    }

    stage('Ansible') {
      steps {
        ansiblePlaybook(playbook: '/ansible-files/test_playbook.yml')
      }
    }

  }
  environment {
    SONARSERVER = 'sonarserver'
  }
}