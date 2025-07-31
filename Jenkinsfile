pipeline {
    agent { label 'dev-john' }

    stages {
        stage('Pull SCM') {
            steps {
                git branch: 'main', url: 'https://github.com/johnsamori/simple-apps.git'
            }
        }
        
        stage('Build') {
            steps {
                sh'''
                cd app
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
                cd app
               sonar-scanner \
                -Dsonar.projectKey=belajar \
                -Dsonar.sources=. \
                -Dsonar.host.url=http://172.23.8.128:9000 \
                -Dsonar.login=sqp_255094158932185ec0c4659a48c906ecaacd6459
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