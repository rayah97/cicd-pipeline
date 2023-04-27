pipeline {
  agent any
  stages {
    stage('Git Checkout') {
      steps {
        git(url: 'https://github.com/rayah97/cicd-pipeline', branch: 'main')
      }
    }

    stage('Build Application') {
      steps {
        sh 'chmod a+x scripts/build.sh'
        sh 'scripts/build.sh'
      }
    }

    stage('Test Application') {
      steps {
        sh 'chmod a+x scripts/test.sh'
        sh 'scripts/test.sh'
      }
    }

    stage('Build Docker Image') {
      steps {
        sh 'docker build -t jenkinsraya .'
      }
    }

    stage('Push Docker Image') {
      steps {
        withCredentials(bindings: [usernamePassword(credentialsId: 'dockerhub', usernameVariable: 'DOCKER_USERNAME', passwordVariable: 'DOCKER_PASSWORD')]) {
          sh "docker login -u $DOCKER_USERNAME -p $DOCKER_PASSWORD"
          sh 'docker tag rayasimage rayahh/my-image:latest'
          sh 'docker push rayahh/jenkinspractice:latest'
        }

      }
    }

  }
  environment {
    PATH = "/opt/homebrew/bin:/usr/local/bin:$PATH"
  }
}