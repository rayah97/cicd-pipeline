pipeline {
  agent any
  stages {
    stage('Git Checkout') {
      steps {
        git(url: 'https://github.com/rayah97/cicd-pipeline', branch: 'main')
      }
    }

    stage('Build app') {
      steps {
        sh '''chmod a+x scripts/build.sh
scripts/build.sh'''
      }
    }

  }
}