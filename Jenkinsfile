pipeline {
    agent any
    
    stages {
        stage('Pull Code') {
            steps {
                git credentialsId: 'mendhe1020', url: 'https://github.com/mendhe1020/nodejs.git'
            }
        }
        
        stage('Install Node.js and npm') {
            steps {
                script {
                    def nodeHome = tool name: 'NodeJS', type: 'jenkins.plugins.nodejs.tools.NodeJSInstallation'
                    env.PATH = "${nodeHome}/bin:${env.PATH}"
                    
                    sh 'node -v'
                    sh 'npm -v'
                }
            }
        }
    }
}
