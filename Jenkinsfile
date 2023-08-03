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

    stage('build jar') {
      steps {
        sh 'mvn package'
      }
    }

    stage('print directory') {
      parallel {
        stage('print directory') {
          steps {
            sh 'ls /target'
          }
        }

        stage('ansible') {
          steps {
            sh 'ansible-playbook -i /ansible-files/inventory.ini /ansible-files/deploy_jar.yml'
          }
        }

      }
    }

  }
  environment {
    ANSIBLE_HOST_KEY_CHECKING = 'False'
  }
}