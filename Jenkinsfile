pipeline {
    agent any

    stages {
        stage('Checkout the repository') {
            steps {
                checkout scm
            }
        }

        stage('Install Node.js') {
            steps {
                sh '''
                    # Update and install prerequisites
                    sudo apt-get update
                    sudo apt-get install -y curl

                    # Add NodeSource and install Node.js 18
                    curl -fsSL https://deb.nodesource.com/setup_18.x | sudo -E bash -
                    sudo apt-get install -y nodejs

                    # Verify installation
                    node -v
                    npm -v
                '''
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }

        stage('Run Tests') {
            steps {
                sh 'npm run test'
            }
        }
    }

    post {
        always {
            echo 'Pipeline completed'
        }
        success {
            echo 'Build succeeded'
        }
        failure {
            echo 'Build failed'
        }
    }
}
