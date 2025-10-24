pipeline {
    agent any
    stages {
        stage('Setup') {
            steps {
                sh '''
                python3 -m venv venv
                . venv/bin/activate
                pip install -r requirements.txt
                '''
            }
        }
        stage('Train Model') {
            steps {
                sh '''
                . venv/bin/activate
                python train_placeholder.py
                '''
            }
        }
        stage('Run Tests') {
            steps {
                sh '''
                . venv/bin/activate
                pytest -q
                '''
            }
        }
        stage('Run App') {
            steps {
                sh '''
                nohup venv/bin/uvicorn app.main:app --host 0.0.0.0 --port 10000 &
                '''
            }
        }
        stage('Sample Prediction') {
            steps {
                sh 'bash test_prediction.sh'
            }
        }
    }
}
