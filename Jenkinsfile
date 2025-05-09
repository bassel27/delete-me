pipeline {
  agent any

  stages {
    stage('Build') {
      steps {
        script {
          docker.image('node:18').inside("-v $WORKSPACE:/app -w /app") {
            sh '''
              npm install
              npm run build -- --configuration=production --project=insight-hub-dashboard
            '''
          }
        }
      }
    }

    stage('Test') {
      steps {
        sh 'test -f insight-hub-dashboard/dist/insight-hub-dashboard/index.html'
      }
    }
  }
}