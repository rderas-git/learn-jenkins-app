pipeline {
    agent any

    environment {
        INDEX_FILE = 'index.html'
    }

    stages {
        stage('Build') {
            agent {
                docker {
                    image 'node:18-alpine'
                    reuseNode true
                }
            }
            steps {
                sh '''
                    ls -la
                    node --version
                    npm --version
                    npm ci
                    npm run build
                    ls -la
                '''
            }
        }
        stage('Test') {
            steps {
                echo 'Testing whether the Index.html file exists ...'
                sh '''
                    test -f build/$INDEX_FILE
                    npm test
                '''
            }
        }
    }
}