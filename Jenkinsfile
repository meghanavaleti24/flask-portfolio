pipeline {
    agent any

    environment {
        APP_DIR = "/home/ubuntu/flask-portfolio"
        VENV_DIR = "${APP_DIR}/venv"
    }

    stages {
        stage('Clone') {
            steps {
                git branch: 'main', url: 'https://github.com/meghanavaleti24/flask-portfolio.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh """
                python3 -m venv ${VENV_DIR}
                source ${VENV_DIR}/bin/activate
                pip install -r requirements.txt
                """
            }
        }

        stage('Restart Flask Service') {
            steps {
                sh 'sudo systemctl restart flask-app'
            }
        }
    }
}
