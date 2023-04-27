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
        sh '''export PATH=/opt/homebrew/bin:$PATH
chmod a+x scripts/build.sh
scripts/build.sh'''
      }
    }

    stage('Run tests') {
      steps {
        sh '''export PATH=/opt/homebrew/bin:$PATH
chmod a+x scripts/test.sh
scripts/test.sh'''
      }
    }

    stage('Build Docker Image') {
      steps {
        sh '''export PATH=$PATH:/usr/local/bin
docker build -t rayasimage .
'''
      }
    }

    stage('Push to Docker Hub') {
      steps {
        withCredentials(bindings: [usernamePassword(credentialsId: 'dockerhub', passwordVariable: 'DOCKERHUB_PASSWORD', usernameVariable: 'DOCKERHUB_USERNAME')]) {
          script {
            withCredentials([dockerLogin(credentialsId: 'dockerhub', url: 'https://hub.docker.com/')]) {
              sh 'docker push rayasimage:latest'
            }
          }

        }

      }
    }

  }
}