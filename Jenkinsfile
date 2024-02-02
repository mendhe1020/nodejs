pipeline {
    agent any

    stages {
        stage('Pull Code') {
            steps {
                // Checkout the source code from the repository
                git 'https://github.com/mendhe1020/nodejs.git/'
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

        stage('Deploy in VM') {
            steps {
                // Add your deployment commands here
                sh 'echo "Deployment in VM"'
                // Example: deploy your application to the VM
                // sh 'npm run deploy'
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
