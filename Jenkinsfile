pipeline {
    agent any
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

        stage('Start Backend Server') {
            steps {
                dir('server') {
                    sh 'npm run server &'
                }
            }
        }

        stage('Start Frontend Server') {
            steps {
                dir('src') {
                    sh 'npm run dev &'
                }
            }
        }
    }

    post {
        success {
            echo 'Application has been built and started successfully.'
        }
        failure {
            echo 'Build failed. Please check the logs for details.'
        }
    }
}
