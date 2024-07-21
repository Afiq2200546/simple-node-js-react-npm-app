pipeline {
    agent any
    
    environment {
        NODE_VERSION = '14.x'
    }

    stages {
        stage('Checkout') {
            steps {
                // Checkout the code from your version control
                checkout scm
            }
        }
        stage('Install Node.js') {
            steps {
                // Install Node.js using Node Version Manager (NVM)
                sh 'curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.1/install.sh | bash'
                sh '. ~/.nvm/nvm.sh && nvm install $NODE_VERSION'
                sh '. ~/.nvm/nvm.sh && nvm use $NODE_VERSION'
            }
        }
        stage('Install Dependencies') {
            steps {
                // Install dependencies
                sh '. ~/.nvm/nvm.sh && npm install'
            }
        }
        stage('Test') {
            steps {
                // Run tests
                sh '. ~/.nvm/nvm.sh && npm test'
            }
        }
        stage('Build') {
            steps {
                // Build the project (if applicable)
                sh '. ~/.nvm/nvm.sh && npm run build'
            }
        }
        stage('Deploy') {
            steps {
                // Deploy the application
                // This is a placeholder. Replace with actual deployment commands
                echo 'Deploying the application...'
                // Example: sh 'scp -r build/ user@server:/path/to/deploy/'
            }
        }
    }
    
    post {
        always {
            // Archive test results and other reports (if applicable)
            junit '**/test-results.xml'
            // Cleanup actions
            echo 'Cleaning up...'
        }
        success {
            echo 'Pipeline succeeded!'
        }
        failure {
            echo 'Pipeline failed!'
        }
    }
}
