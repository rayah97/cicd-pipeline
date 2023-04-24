pipeline {
  agent any
  stages {
    stage('Git Checkout') {
      steps {
        git(url: 'https://github.com/rayah97/cicd-pipeline', branch: 'main')
      }
    }

    stage('Build image') {
      steps {
        script {
          sh 'docker build -t myapp .'
        }

      }
    }

  }
}