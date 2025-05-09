pipeline {
    agent none // Changed from 'any' to 'none' since we define agents per stage

    stages {
        stage('Initialize') {
            agent any
            steps {
                script {
                    def dockerHome = tool 'myDocker'
                    env.PATH = "${dockerHome}/bin:${env.PATH}"
                }
            }
        }

        stage('Build') {
            agent {
                docker {
                    image 'node:18'
                }
            }
            steps {
                sh '''
                    cd insight-hub-dashboard
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