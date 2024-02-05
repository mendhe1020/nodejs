pipeline {
    agent any

    stages {
        stage('Pull Code') {
            steps {
                script {
                    // Step 1: Pull the code from the 'Staging' branch
                    checkout scm
                }
            }
        }
        stage('Install Node.js and npm') {
            steps {
                script {
                    try {
                        // Step 2: Install Node.js and npm
                        sh '''
                            curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.1/install.sh | bash
                            export NVM_DIR="$HOME/.nvm"
                            [ -s "$NVM_DIR/nvm.sh" ] && . "$NVM_DIR/nvm.sh"
                            [ -s "$NVM_DIR/bash_completion" ] && . "$NVM_DIR/bash_completion"
                            nvm install node # Install the latest version of Node.js
                            npm install -g npm # Install the latest version of npm
                        '''
                    } catch (Exception e) {
                        // Catch and handle any errors during installation
                        echo "Error during Node.js and npm installation: ${e.message}"
                        currentBuild.result = 'FAILURE'
                        error("Failed to install Node.js and npm")
                    }
                }
            }
        }
    }
}
