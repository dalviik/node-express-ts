pipeline {
    agent any
    
    stages {
        stage('Build') {
            steps {
                sh 'npm run build'
            }
            post {
                always {
                    
                    sh 'pwd'
                    sh 'javac '
                    
                }
            }
        },
       
    }
}