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

    stage('Ansible') {
      steps {
        sh 'ansible-playbook -i /ansible-files/inventory.ini /ansible-files/deploy_jar.yml'
      }
    }

  }
  environment {
    ANSIBLE_HOST_KEY_CHECKING = 'False'
  }
}