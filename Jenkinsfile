pipeline {
    agent any
    
    stages {
        stage('Pull Code') {
            steps {
                // Checkout the source code from the repository
                git branch: '*/Staging', credentialsId: 'mendhe1020', url: 'https://github.com/mendhe1020/nodejs.git'
            }
        }

        stage('Install Node.js and npm') {
            steps {
                script {
                    // Install Node.js using the NodeJS Jenkins plugin
                    // 'nodejs' should match the tool name you configured in Jenkins
                    def nodejsInstallation = tool name: 'nodejs', type: 'jenkins.plugins.nodejs.tools.NodeJSInstallation'
                    def nodejsHome = "${nodejsInstallation}/bin"
                    env.PATH = "${nodejsHome}:${env.PATH}"

                    // Install npm version 8 globally
                    sh 'npm install -g npm@8'
                }
            }
        }

        stage('Deploy to Staging') {
            when {
                branch 'Staging'
            }
            steps {
                // Add deployment steps specific to the Staging environment
                sh 'echo "Deploying to Staging"'
            }
        }

        stage('Deploy to Development') {
            when {
                branch 'development'
            }
            steps {
                // Add deployment steps specific to the Development environment
                sh 'echo "Deploying to Development"'
            }
        }

        stage('Deploy to Production') {
            when {
                branch 'production'
            }
            steps {
                // Add deployment steps specific to the Production environment
                sh 'echo "Deploying to Production"'
            }
        }
    }

    post {
        success {
            echo 'Deployment successful'
        }
        failure {
            echo 'Deployment failed'
        }
    }
}
