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
                    sh """
                        ssh -o StrictHostKeyChecking=no $REMOTE_USER@$REMOTE_HOST << EOF
                            cd $APP_DIR
                            if [ ! -d "venv" ]; then
                                python3 -m venv venv
                            fi
                            source venv/bin/activate
                            pip install -r requirements.txt
                            sudo systemctl restart flask-app
                        EOF
                    """
                }
            }
        }
    }
}
