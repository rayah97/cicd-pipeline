pipeline {
  agent any
  stages {
    stage('Git Checkout') {
      steps {
        git(url: 'https://github.com/rayah97/cicd-pipeline', branch: 'main')
      }
    }

    stage('Build Image') {
      steps {
        sh '''docker build -t imagefromraya .
'''
      }
    }

  }
}