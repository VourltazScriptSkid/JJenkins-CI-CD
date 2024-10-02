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
                // Capture the log and write it to a file using forward slashes
                def logFile = "${env.WORKSPACE}/pipeline-log.txt"
                writeFile file: logFile, text: currentBuild.getLog().join("\n")
            }
            echo 'Pipeline complete.'
        }

        success {
            echo 'Pipeline succeeded!'
            emailext to: 'andreiangeles738@gmail.com',
                     subject: "Jenkins Pipeline Success: ${env.JOB_NAME}",
                     body: "The Jenkins pipeline ${env.JOB_NAME} completed successfully. Logs are attached.",
                     attachmentsPattern: "**/pipeline-log.txt"  // Use a GLOB pattern to match the file
        }

        failure {
            echo 'Pipeline failed!'
            emailext to: 'andreiangeles738@gmail.com',
                     subject: "Jenkins Pipeline Failure: ${env.JOB_NAME}",
                     body: "The Jenkins pipeline ${env.JOB_NAME} failed. Logs are attached.",
                     attachmentsPattern: "**/pipeline-log.txt"  // Use a GLOB pattern to match the file
        }
    }
}
