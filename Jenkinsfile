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
        sh '''sh \'curl -sL "https://deb.nodesource.com/setup_lts.x" | sudo -E bash -\'
sh \'sudo apt-get install -y nodejs\'
sh \'sudo npm install -g npm@latest\''''
      }
    }

  }
}