pipeline {
    agent any

    stages {
        stage('Build'){
            agent {
                docker {
                    image 'node:18-alpine'
                    args '-u root:root'
                    reuseNode true
                }
            }
            steps {
                sh '''
                  ls -la
                  node --version
                  npm install -g npm@6
                  npm ci
                  npm run build
                  ls -la
                '''
            }

        }
        stage('Test'){
            agent 
            {
                docker {
                    image "node:18-alpine"
                    args '-u root:root'
                    reuseNode true
                }
            }
            steps {
            sh '''
             test -f build/index.html
             npm test
            '''
        }
        }
        
    }
    post {
        always {
            junit 'test-results/junit.xml'
        }
    }
}