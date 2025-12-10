pipeline {
    agent any

    tools {
        nodejs "NodeJS2500"   // 👈 use the NodeJS tool you created
    }

    environment {
        REPO_URL = "http://git-server:3000/max/node-app.git"
    }

    stages {

        stage('Checkout Code') {
            steps {
                git branch: 'main', url: "${REPO_URL}"
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }

        stage('Run App') {
            steps {
                sh 'node app.js &'
                echo "App started on ports 3001 and 3002"
            }
        }

        stage('Archive Artifacts') {
            steps {
                archiveArtifacts artifacts: '**/*.js', fingerprint: true
            }
        }
    }

    post {
        success {
            echo "Build succeeded"
        }
        failure {
            echo "Build failed"
        }
    }
}
