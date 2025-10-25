pipeline {
    agent any

    environment {
        // Full Python paths (to avoid PATH issues for Jenkins service)
        PYTHON_EXE = "C:\\Users\\win10\\AppData\\Local\\Programs\\Python\\Python312\\python.exe"
        PIP_EXE = "C:\\Users\\win10\\AppData\\Local\\Programs\\Python\\Python312\\Scripts\\pip.exe"
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
                bat "\"%PYTHON_EXE%\" --version"
                bat "\"%PIP_EXE%\" --version"
            }
        }

        stage('Install Dependencies') {
            steps {
                echo 'Installing required packages...'
                bat "\"%PIP_EXE%\" install --upgrade pip"
                bat "\"%PIP_EXE%\" install -r requirements.txt"
            }
        }

        stage('Run Tests / App') {
            steps {
                echo 'Running sample test (train placeholder)...'
                bat "\"%PYTHON_EXE%\" train_placeholder.py"
            }
        }

        stage('Post Build') {
            steps {
                echo '✅ Build and training finished successfully.'
            }
        }
    }

    post {
        success {
            echo '🎉 Build Succeeded!'
        }
        failure {
            echo '❌ Build failed!'
        }
    }
}
