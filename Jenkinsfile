pipeline {
    agent none // Changed from 'any' to 'none' since we define agents per stage

    stages {
        stage('Build') {
            agent {
                docker {
                    image 'node:18'
                    args '-v $WORKSPACE:/app -w /app' // Mount workspace and set working directory
                }
            }
            steps {
                sh '''
                    npm ci
                    npm run build -- --configuration=production --project=insight-hub-dashboard
                '''
            }
        }

        stage('Test') {
            agent any // Runs on any available agent (no Docker required)
            steps {
                sh 'test -f insight-hub-dashboard/dist/insight-hub-dashboard/index.html' // Fixed path to likely build output
            }
        }
    }
}