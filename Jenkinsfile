pipeline {
    agent any

    stages {
        stage('Checkout the repository') {
            steps {
                checkout scm
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }

        stage('Audit & Test in Parallel') {
            parallel {
                stage('Security Audit') {
                    steps {
                        sh 'npm audit'
                    }
                }

                stage('Run Tests') {
                    steps {
                        sh 'npm run test'
                    }
                }
            }
        }

        stage('Deploy') {
            steps {
                input message: 'Approve deployment?', ok: 'Deploy'
                sh 'echo Deploying application...'  // Replace this with real deploy command
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