pipeline {
    agent any

    environment {
        FRONTEND_DIR = 'src'
        BACKEND_DIR = 'server'
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/Dhoble10/chatapp-master.git', credentialsId: '20e9b267-e8f7-410b-84ee-c59dd65ba49c'
            }
        }

        stage('Install Dependencies') {
            parallel {
                stage('Frontend') {
                    steps {
                        dir("${env.FRONTEND_DIR}") {
                            bat 'npm install'
                        }
                    }
                }
                stage('Backend') {
                    steps {
                        dir("${env.BACKEND_DIR}") {
                            bat 'npm install'
                        }
                    }
                }
            }
        }

        stage('Build Frontend') {
            steps {
                dir("${env.FRONTEND_DIR}") {
                    bat 'npm run build'
                }
            }
        }

        stage('Start Servers (Optional for Testing)') {
            steps {
                echo 'Starting backend and frontend servers...'
                bat "start /B cmd /c \"cd ${env.BACKEND_DIR} && npm run server\""
                bat "start /B cmd /c \"cd ${env.FRONTEND_DIR} && npm start\""
            }
        }
    }

    post {
        success {
            echo '✅ Application built and started successfully.'
        }
        failure {
            echo '❌ Build failed. Check the logs for more details.'
        }
        always {
            echo '🧹 Cleaning up node processes (if any)...'
            bat 'taskkill /F /IM node.exe || echo "No node processes to kill."'
        }
    }
}
