pipeline{
    agent any

    environment {
        NETLIFY_SITE_ID = '8f96ab13-92ed-4352-9ddf-449978169f83'
        NETLIFY_AUTH_TOKEN = credentials('netlify-token')
    }
        stages{
            stage('build'){
                agent {
                    docker{
                        image 'node:18-alpine'
                        reuseNode true
                    }
                }
                steps{
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
            stage('test webhook github '){
                agent {
                    docker{
                        image 'node:18-alpine'
                        reuseNode true
                    }
                }
                steps{
                    sh '''test -f build/index.html
                        npm test
                    
                    '''
                }
            }
            stage('deploy'){
                agent {
                    docker{
                        image 'node:18-alpine'
                        reuseNode true
                    }
                }
                steps{
                    sh '''
                        npm install netlify-cli
                        node_modules/.bin/netlify --version
                        echo "deploying to site id : $8f96ab13-92ed-4352-9ddf-449978169f83"
                        node_modules/.bin/netlify status
                        
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