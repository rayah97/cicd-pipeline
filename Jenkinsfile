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
        sh '''source ~/.bash_profile
/opt/homebrew/bin/npm install
chmod a+x scripts/build.sh
scripts/build.sh'''
      }
    }

    stage('Run tests') {
      steps {
        sh '''chmod a+x scripts/test.sh
scripts/test.sh'''
      }
    }

    stage('Build Docker Image') {
      steps {
        sh '''docker build -t rayasimage .
'''
      }
    }

  }
}