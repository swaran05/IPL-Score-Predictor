pipeline {
    agent any

    environment {
        // Set Python path manually (important for Windows Jenkins)
        PATH = "C:\\Users\\win10\\AppData\\Local\\Programs\\Python\\Python312\\;C:\\Users\\win10\\AppData\\Local\\Programs\\Python\\Python312\\Scripts\\;%PATH%"
    }

    stages {

        stage('Checkout') {
            steps {
                echo 'Checking out code...'
                checkout scm
            }
        }

        stage('Setup Python') {
            steps {
                echo 'Checking Python installation...'
                bat 'python --version'
                bat 'pip --version'
            }
        }

        stage('Install Dependencies') {
            steps {
                echo 'Installing dependencies...'
                // assumes you have requirements.txt in your repo
                bat 'pip install --upgrade pip'
                bat 'pip install -r requirements.txt'
            }
        }

        stage('Run Tests / App') {
            steps {
                echo 'Running FastAPI app for verification...'
                // If your main app file is app/main.py
                bat 'python app/main.py'
            }
        }

        stage('Post Build') {
            steps {
                echo '✅ Build complete!'
            }
        }
    }

    post {
        success {
            echo 'Build succeeded!'
        }
        failure {
            echo '❌ Build failed!'
        }
    }
}
