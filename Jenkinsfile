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
    stage('Image Build') {
      steps {
        script {
          def customImage = docker.build("${registry}:${env.BUILD_ID}")
        }

      }
    }
    stage('Build Docker Image') {
      steps {
        sh 'docker build -t rayasimage .'
      }
    }

    stage('Push Image') {
      steps {
        script {
          docker.withRegistry('', 'dockerhub-id') {
            docker.image("${registry}:${env.BUILD_ID}").push('latest')
            docker.image("${registry}:${env.BUILD_ID}").push("${env.BUILD_ID}")
          }
        }

      }
    }

  }
  environment {
    registry = 'rayahh/jenkinspractice'
  }
}
