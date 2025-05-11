pipeline {
    agent any

    stages {
        stage('Build') {
            agent {
                docker {
                    image 'node:18'
                }
            }
            steps {
                sh '''
                    npm install
                    npm run build -- --configuration=production
                '''
            }
        }

        stage('Test') {
            agent any
            steps {
                sh 'test -f insight-hub-dashboard/dist/insight-hub-dashboard/index.html'
            }
        }
    }
}