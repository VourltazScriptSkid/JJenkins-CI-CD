pipeline {
    agent any

    stages {
        stage('Checkout SCM') {
            steps {
                checkout scm
            }
        }

        stage('Build') {
            steps {
                echo 'Building the application...'
                bat 'echo Build complete'
            }
        }

        stage('Test') {
            steps {
                echo 'Running tests...'
                bat 'echo Tests complete'
            }
        }

        stage('Code Analysis') {
            steps {
                echo 'Performing code analysis...'
                echo 'Tool used: SonarQube'
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying the application...'
                bat 'echo Deployment complete'
            }
        }
    }

    post {
        always {
            script {
                // Use getRawBuild() to capture the log
                def logFile = "${env.WORKSPACE}/pipeline-log.txt"
                writeFile file: logFile, text: currentBuild.rawBuild.getLog(1000).join("\n") // Captures the last 1000 lines
            }
            echo 'Pipeline complete.'
        }

        success {
            echo 'Pipeline succeeded!'
            emailext to: 'andreiangeles738@gmail.com',
                     subject: "Jenkins Pipeline Success: ${env.JOB_NAME}",
                     body: "The Jenkins pipeline ${env.JOB_NAME} completed successfully. Logs are attached.",
                     attachmentsPattern: "**/pipeline-log.txt"
        }

        failure {
            echo 'Pipeline failed!'
            emailext to: 'andreiangeles738@gmail.com',
                     subject: "Jenkins Pipeline Failure: ${env.JOB_NAME}",
                     body: "The Jenkins pipeline ${env.JOB_NAME} failed. Logs are attached.",
                     attachmentsPattern: "**/pipeline-log.txt"
        }
    }
}
