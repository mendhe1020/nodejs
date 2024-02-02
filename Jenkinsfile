pipeline {
    agent any

    stages {
        stage('Pull Code') {
            steps {
                // Checkout the code from the Git repository
                git branch: 'master', credentialsId: 'mendhe1020', url: 'https://github.com/mendhe1020/nodejs.git'
            }
        }

        stage('Install Node.js and npm') {
            steps {
                script {
                    // Install Node.js using the NodeJS Jenkins plugin
                    def nodejsInstallation = tool name: 'nodejs', type: 'jenkins.plugins.nodejs.tools.NodeJSInstallation'
                    def nodejsHome = "${nodejsInstallation}/bin"
                    env.PATH = "${nodejsHome}:${env.PATH}"

                    // Install npm version 8 globally
                    sh 'npm install -g npm@8'
                }
            }
        }

        stage('Start Node.js Service') {
            steps {
                // Start the Node.js service
                sh 'node app.js &'  // Assuming your Node.js application entry point is app.js
            }
        }
    }

    post {
        success {
            echo 'All steps executed successfully'
        }
        failure {
            echo 'One or more steps failed'
        }
    }
}
