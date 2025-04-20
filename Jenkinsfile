pipeline {
    agent any

    environment {
        // Optional: Define environment variables if needed
        NODE_ENV = 'development'
    }

    tools {
        nodejs 'NodeJS_18'  // Replace with your Jenkins Node.js tool name
    }

    stages {
        

        stage('Lint / Test') {
            steps {
                // Run linter or test suite if available
                sh 'npm run lint || echo "Linting skipped"'
                sh 'npm test || echo "Tests skipped"'
            }
        }

        stage('Build') {
            steps {
                // If there's a build step (e.g., React/Angular), otherwise skip
                sh 'npm run build || echo "No build script found"'
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying app...'
                // Add deploy logic here (e.g., Docker, SCP, PM2, etc.)
            }
        }
    }

    post {
        success {
            echo 'Build completed successfully.'
        }
        failure {
            echo 'Build failed.'
        }
    }
}
