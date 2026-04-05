pipeline {
    agent any
    stages {
        stage('Logging') {
            steps {
                sh 'echo Hello from devesh side'
            }
        }

        stage('build') {
            agent {
                docker {
                    image 'node:18-alpine'
                    reuseNode true
                }
            }
            steps {
                sh 'npm --version'
                sh 'ls -la'
                sh 'npm ci'
                sh 'ls -la'
                sh 'npm run build'
            }
        }

        stage('test') {
            agent {
                docker {
                    image 'node:18-alpine'
                    reuseNode true
                }
            }
            steps {
                sh 'test -f build/index.html'
                sh 'CI=true npm test'
            }
        }
    }
    post {
        always {
            junit testResults: 'test-results/junit.xml', allowEmptyResults: true
        }
    }
}
