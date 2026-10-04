pipeline {
    agent any

    environment {
        DEPLOY_DIR = 'C:\\inetpub\\wwwroot\\event-registration'
    }

    stages {
        stage('Checkout') {
            steps {
                echo 'Fetching code from GitHub...'
                checkout scm
            }
        }

        stage('Build') {
            steps {
                echo 'Building the Event Registration Form...'
                bat 'dir'
            }
        }

        stage('Test') {
            steps {
                echo 'Running basic tests...'

                bat 'if not exist index.html exit /b 1'
                bat 'if not exist style.css exit /b 1'
                bat 'if not exist script.js exit /b 1'

                bat 'findstr /C:"<form" index.html >nul || exit /b 1'
                echo 'Form tag present'

                bat 'findstr /C:"addEventListener" script.js >nul || exit /b 1'
                echo 'Validation script present'
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying to web server...'

                bat 'if not exist "%DEPLOY_DIR%" mkdir "%DEPLOY_DIR%"'

                bat 'copy /Y index.html "%DEPLOY_DIR%\\"'
                bat 'copy /Y style.css "%DEPLOY_DIR%\\"'
                bat 'copy /Y script.js "%DEPLOY_DIR%\\"'

                echo 'Deployed at http://localhost/event-registration/'
            }
        }
    }

    post {
        success {
            echo 'Pipeline completed successfully!'
        }

        failure {
            echo 'Pipeline failed. Check the logs.'
        }
    }
}
