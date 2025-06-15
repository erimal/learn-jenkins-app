pipeline {
    agent any

    stages {
    /*
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
        */

        stage ('Test stage') {
            agent {
                docker {
                    image 'node:18-alpine'
                    reuseNode true
                }
            }
            steps{
                sh '''
                    echo "Test Stage"
                    #find build/ -name "index.html"
                    #npm test

                '''

            }
        }
        stage('E2E') {
            agent {
                docker {
                   # image 'mcr.microsoft.com/playwright:v1.39.0-jammy'
                    image 'mcr.microsoft.com/playwright:v1.59.0-jammy'
                    reuseNode true
                }
            }
            steps {
                sh '''
                    npm install serve
                    node_modules/.bin/serve -s build &
                    sleep 10
                    npx playwright test
                '''
            }
        }




    }
    post{
        always{
            junit 'jjest-results/junit.xml'
        }
    }
}