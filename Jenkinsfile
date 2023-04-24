pipeline {
  agent any
  stages {
    stage('Git Checkout') {
      steps {
        git(url: 'https://github.com/rayah97/cicd-pipeline', branch: 'main')
      }
    }

    stage('') {
      steps {
        sh '''scripts/test.sh
'''
      }
    }

  }
}