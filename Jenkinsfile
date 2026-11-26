pipeline {
    agent { label 'prod-devops1' }

    stages {
        stage('Pull SCM') {
            steps {
                git branch: 'main', url: 'https://github.com/buangyulianto/simple-apps.git'
            }
        }
        
        stage('Build') {
            steps {
                sh'''
                cd apps
                npm install
                '''
            }
        }
        
        stage('Testing') {
            steps {
                dir('apps') {
                    sh'''
                    npm test
                    npm run test:coverage
                    '''
                }
            }
        }
        
        stage('Code Review') {
            steps {
                dir('apps') {
                    sh'''
                    sonar-scanner \
                        -Dsonar.projectKey=test-apps1 \
                        -Dsonar.sources=. \
                        -Dsonar.host.url=http://172.23.8.155:9000 \
                        -Dsonar.login=sqp_c18c569fdd4fb1171509ef334b4ee30dd1acc192
                    '''
                }
            }
        }
        
        stage('Deploy') {
            steps {
                sh'''
                docker compose up --build -d
                '''
            }
        }
        
        stage('Backup') {
            steps {
                 sh 'docker compose push' 
            }
        }
    }
}