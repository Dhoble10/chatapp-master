pipeline {
    agent any

    tools {
        nodejs 'NodeJS_18' // Make sure this matches your configured Jenkins Node.js tool name
    }

    environment {
        NODE_ENV = 'development'
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/Dhoble10/chatapp-master.git', credentialsId: '20e9b267-e8f7-410b-84ee-c59dd65ba49c'
            }
        }

        stage('Install Frontend Dependencies') {
            steps {
                dir('src') {
                    sh 'npm install'
                }
            }
        }

        stage('Build Frontend') {
            steps {
                dir('src') {
                    sh 'npm run build'
                }
            }
        }

        stage('Install Backend Dependencies') {
            steps {
                dir('server') {
                    sh 'npm install'
                }
            }
        }

        // Optional: Add test stages here if available

        // Deployment or Run step should not be backgrounded in a Jenkins pipeline.
        // Use proper tools if needed (Docker, PM2, etc.)

    }

    post {
        success {
            echo '✅ Build completed successfully.'
        }
        failure {
            echo '❌ Build failed. Check the logs.'
        }
    }
}
