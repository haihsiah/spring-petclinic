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

        stage('print directory') {
          steps {
            sh 'ls'
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
        stage('print current dir') {
          steps {
            sh '''ls
ls target'''
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