environment {
    FRONTEND_DIR = 'src'
    BACKEND_DIR = 'server'
    DEPLOY_USER = 'ubuntu'
    DEPLOY_HOST = 'your-ec2-public-ip' // replace with your EC2 IP
    DEPLOY_DIR  = '/home/ubuntu/chatapp-master'
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

    stage('Deploy to EC2') {
        steps {
            echo '🚀 Deploying to AWS EC2...'
            sshagent (credentials: ['ec2-ssh-key']) {
                sh """
                    ssh -o StrictHostKeyChecking=no ${DEPLOY_USER}@${DEPLOY_HOST} '
                        cd ${DEPLOY_DIR} &&
                        git pull origin main &&
                        docker-compose down &&
                        docker-compose build --no-cache &&
                        docker-compose up -d
                    '
                """
            }
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
