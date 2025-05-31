pipeline {
    agent any

    environment {
        SAG_HOME = "C:\\SoftwareAG"
        PACKAGE = "myPackage"
        IS_PACKAGES = "${SAG_HOME}\\IntegrationServer\\instances\\default\\packages"
    }

    stages {
        stage('Deploy Package') {
            steps {
                sh '''
                    echo "Deploying package..."
                    cp -r myPackage "$IS_PACKAGES"
                '''
            }
        }
        stage('Reload Package') {
            steps {
                // Replace this with a Unix-style curl command since you're using `sh` not `bat`
                sh '''
                    echo "Reloading package..."
                    curl -u Administrator:manage -X POST "http://host.docker.internal:5555/invoke/wm.server.packages:reload?package=myPackage"
                '''
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
