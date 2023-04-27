pipeline {
  agent any
  environment {
    PATH = "/opt/homebrew/bin:/usr/local/bin:$PATH"
  }
  stages {
    stage('Git Checkout') {
      parallel {
        stage('Git Checkout') {
          steps {
            git(url: 'https://github.com/rayah97/cicd-pipeline', branch: 'main')
          }
        }

        stage('User Check') {
          steps {
            sh 'whoami'
          }
        }
      }
    }

    stage('Build App') {
      steps {
        sh 'chmod a+x scripts/build.sh'
        sh 'scripts/build.sh'
      }
    }

    stage('Run Tests') {
      steps {
        sh 'chmod a+x scripts/test.sh'
        sh 'scripts/test.sh'
      }
    }

    stage('Build Docker Image') {
      steps {
        sh 'docker build -t rayasimage .'
      }
    }

    stage('Push Docker') {
      steps {
        withCredentials([usernamePassword(credentialsId: 'dockerhub', usernameVariable: 'DOCKER_USERNAME', passwordVariable: 'DOCKER_PASSWORD')]) {
          sh "docker login -u $DOCKER_USERNAME -p $DOCKER_PASSWORD"
          sh 'docker tag rayasimage rayahh/my-image:latest'
          sh 'docker push rayahh/my-image:latest'
        }
      }
    }
  }
}
