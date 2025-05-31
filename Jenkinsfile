pipeline {
    agent any

    environment {
        SAG_HOME = "C:\\SoftwareAG"
        PACKAGE = "myDemoPackage"
        IS_PACKAGES = "${SAG_HOME}\\IntegrationServer\\instances\\default\\packages"
    }

    stages {
        stage('Clone Repo') {
            steps {
                git 'https://github.com/Danish2511/myPackage.git'
            }
        }

        stage('Deploy Package') {
            steps {
                bat """
                xcopy /E /Y "%WORKSPACE%\\*" "${IS_PACKAGES}\\%PACKAGE%\\"
                """
            }
        }

        stage('Reload Package') {
            steps {
                bat """
                curl -u Administrator:manage -X POST "http://localhost:5555/invoke/wm.server.packages:reload?package=%PACKAGE%"
                """
            }
        }
    }

    post {
        success {
            echo '✅ Package Deployed and Reloaded!'
        }
        failure {
            echo '❌ Deployment Failed.'
        }
    }
}
