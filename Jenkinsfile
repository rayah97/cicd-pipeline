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

    stage('Push to Docker Hub') {
      steps {
        withCredentials([usernamePassword(credentialsId: 'dockerhub', passwordVariable: 'Raya.199727', usernameVariable: 'rayahh')]) {
          script {
            sh 'export PATH=$PATH:/usr/local/bin'

            docker login -u $DOCKERHUB_USERNAME -p $DOCKERHUB_PASSWORD
            docker tag rayasimage $DOCKERHUB_USERNAME/rayasimage:$BUILD_NUMBER
            docker push $DOCKERHUB_USERNAME/rayasimage:$BUILD_NUMBER
          }
        }
      }
    }
  }
}
