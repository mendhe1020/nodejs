pipeline {
    agent any

    stages {
        stage('Pull Code') {
            steps {
                // Step 1: Pull the code into VM
                git 'https://github.com/mendhe1020/nodejs.git/'
            }
        }
        stage('Install Node.js and npm') {
            steps {
                // Step 2: Install Node.js and npm and start the service
                script {
                    // Example: Using nvm to manage Node.js versions
                    // You can adjust this according to your setup
                    sh '''
                        curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.1/install.sh | bash
                        export NVM_DIR="$HOME/.nvm"
                        [ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh"
                        [ -s "$NVM_DIR/bash_completion" ] && \. "$NVM_DIR/bash_completion"
                        nvm install node # Install the latest version of Node.js
                        npm install -g npm # Install the latest version of npm
                    '''
                }
            }
        }
    }
}
