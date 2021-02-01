pipeline {
    agent any
    
    stages {
        stage('Build') {
            steps {
                sh 'echo `INSTALANDO DEPENDENCIAS`'
                sh 'pwd'
                sh 'npm install'
                
            }
            post {
                always {
                    sh 'echo `BUILD`'
                    sh 'npm run build'
                    
                }
            }
        }
       
    }
}