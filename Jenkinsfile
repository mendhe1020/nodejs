pipeline {
    agent any
    
    stages {
        stage('Checkout') {
            steps {
                // Checkout code from the repository
                git branch: "${env.BRANCH_NAME}", url: 'https://github.com/mendhe1020/nodejs.git'
            }
        }
        stage('Build') {
            steps {
                // Replace this with your build commands
                sh 'npm install'
            }
        }
        stage('Test') {
            steps {
                // Replace this with your test commands
                sh 'npm test'
            }
        }
        stage('Deploy') {
            steps {
                // Replace this with your deployment commands
                sh 'npm run deploy'
            }
        }
    }
    
    post {
        success {
            echo 'Pipeline succeeded! Yay!'
        }
        failure {
            echo 'Pipeline failed! Oh no!'
        }
        always {
            // This block will always be executed, regardless of the pipeline's outcome
            echo 'Cleaning up...'
        }
    }
}
