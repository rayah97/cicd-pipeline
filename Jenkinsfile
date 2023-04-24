pipeline {
  agent any
  stages {
    stage('Git Checkout') {
      steps {
        git(url: 'https://github.com/rayah97/cicd-pipeline', branch: 'main')
      }
    }

    stage('Build') {
      steps {
        sh '''sh \'curl -sL https://deb.nodesource.com/setup_lts.x | bash -\'
sh \'apt-get install -y nodejs\'
sh \'npm install -g npm@latest\''''
      }
    }

  }
}