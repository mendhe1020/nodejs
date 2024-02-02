pipeline {
    agent any

    environment {
       # SSH_KEY = credentials('8080aedc-a4ad-4e48-b31b-90001c0d1eb4')
       # TARGET_SERVER = 'ubuntu@35.171.18.189'
        BASE_TARGET_DIR = '/home/ubuntu'
    }

    stages {
        stage('Deploy to Target Server') {
            steps {
                script {
                    // Copy SSH key to Jenkins user's home directory
                    sh "sudo cp /root/.ssh/id_rsa /var/lib/jenkins/.ssh/"
                    sh "sudo chown jenkins:jenkins /var/lib/jenkins/.ssh/id_rsa"

                    // Create an SSH configuration file to disable strict host key checking
                    sh 'echo "Host *\n  StrictHostKeyChecking no" > /var/lib/jenkins/.ssh/config'

                    // Use ssh-agent to run the SSH command
                    sshagent(credentials: [SSH_KEY]) {
                        // Run the command as the jenkins user without sudo
                        sh "ssh -i /var/lib/jenkins/.ssh/id_rsa ${TARGET_SERVER} 'mkdir -p ${BASE_TARGET_DIR}/${env.BRANCH_NAME.toLowerCase()}'"
                    }
                }
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

        stage('Deploy Node.js Project') {
            steps {
                script {
                    // Assuming your Node.js project is in the current workspace
                    def workspace = pwd()

                    // Use rsync to copy the project to the target server
                    sh "rsync -r -e 'ssh -i /var/lib/jenkins/.ssh/id_rsa' ${workspace}/ ${TARGET_SERVER}:${BASE_TARGET_DIR}/${env.BRANCH_NAME.toLowerCase()}/"
                }
            }
        }

        Post 
        {
            always
            {
              emailext body: 'yee!', subject: 'regarding cicd pipeline', to: 'anurag.mendhe11@gmail.com'
            }
        }
    }
}
