pipeline {
  agent any
  stages {
    stage('Git Checkout') {
      parallel {
        stage('Git Checkout') {
          steps {
            git(url: 'https://github.com/rayah97/cicd-pipeline', branch: 'main')
          }
        }

        stage('usercheck') {
          steps {
            sh 'whoami'
          }
        }

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

    stage('Push') {
      steps {
        script {
          withCredentials([usernamePassword(credentialsId: 'dockerhub', usernameVariable: 'rayahh', passwordVariable: 'Raya.199727')]) {
            sh "docker login -u $rayahh -p $Raya.199727"
          }
          sh 'docker tag rayasimage rayahh/my-image:latest'
          sh 'docker push rayahh/my-image:latest'
        }

      }
    }

  }
}