pipeline {
    agent any

    environment {
        REMOTE_USER = "ubuntu"
        REMOTE_HOST = "18.233.166.221"
        APP_DIR = "/home/ubuntu/flask-portfolio"
        VENV_DIR = "${APP_DIR}/venv"
    }

    stages {
        stage('Deploy to Flask App EC2') {
            steps {
                sshagent(credentials: ['flask-app-key']) {
                    script {
                        sh "ssh -o StrictHostKeyChecking=no $REMOTE_USER@$REMOTE_HOST 'cd $APP_DIR && git pull origin main'"
                        sh "ssh -o StrictHostKeyChecking=no $REMOTE_USER@$REMOTE_HOST 'if [ ! -d \"$VENV_DIR\" ]; then python3 -m venv $VENV_DIR; fi'"
                        sh "ssh -o StrictHostKeyChecking=no $REMOTE_USER@$REMOTE_HOST 'source $VENV_DIR/bin/activate && pip install -r $APP_DIR/requirements.txt'"
                        sh "ssh -o StrictHostKeyChecking=no $REMOTE_USER@$REMOTE_HOST 'sudo systemctl restart flask-app'"
                    }
                }
            }
        }
    }
}
