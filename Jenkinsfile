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
                sh'''
                cd app
                npm test
                npm run test:coverage
                '''
            }
        }
        
        stage('Code Review') {
            steps {
                sh'''
                cd apps
                sonar-scanner \
                    -Dsonar.projectKey=Simple-Apps \
                    -Dsonar.sources=. \
                    -Dsonar.host.url=http://172.23.8.155:9000 \
                    -Dsonar.login=sqp_1890b551d35033c61ff8cd453cec9333cfa9d0a6
                '''
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