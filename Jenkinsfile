pipeline {
    agent any

    stages {
        stage('Checkout the repository') {
            steps {
                checkout scm
            }
        }

        stage('Install Node.js on Debian') {
            steps {
                sh '''
                    # Install curl if not present
                    if ! command -v curl > /dev/null; then
                        apt-get update
                        apt-get install -y curl
                    fi

                    # Add Node.js 18.x from NodeSource
                    curl -fsSL https://deb.nodesource.com/setup_18.x | bash -
                    apt-get install -y nodejs

                    # Confirm installation
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
