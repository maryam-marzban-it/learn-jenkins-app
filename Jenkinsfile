pipeline{
    agent any
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
            stage('test'){
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
                        npm install -g netlify-cli
                        netlify --version
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