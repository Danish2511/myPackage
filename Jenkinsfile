pipeline {
    agent any

    environment {
        PACKAGE = "myPackage"
        IS_PACKAGES = "/opt/sag-packages" // Path inside container
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
