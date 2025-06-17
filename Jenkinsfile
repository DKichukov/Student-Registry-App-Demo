pipeline {
    agent any

    environment {
        NODE_VERSION = '20.14.0'
        INSTALL_DIR = "${env.HOME}/local/node-v${NODE_VERSION}"
        PATH = "${env.HOME}/local/node-v${NODE_VERSION}/bin:${env.PATH}"
    }

    stages {
        stage('Checkout the repository') {
            steps {
                checkout scm
            }
        }

        stage('Install Node.js (non-root)') {
            steps {
                sh '''
                    set -e

                    # Create target install directory
                    mkdir -p "$INSTALL_DIR"

                    # Download and extract Node.js tarball
                    curl -fsSL https://nodejs.org/dist/v$NODE_VERSION/node-v$NODE_VERSION-linux-x64.tar.gz \
                        | tar -xz --strip-components=1 -C "$INSTALL_DIR"

                    # Verify
                    "$INSTALL_DIR/bin/node" -v
                    "$INSTALL_DIR/bin/npm" -v
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
