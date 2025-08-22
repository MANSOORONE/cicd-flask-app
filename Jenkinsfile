pipeline {
    agent any
    stages {
        stage('Clone Code') {
            steps {
                git branch: 'main', url: 'https://github.com/MANSOORONE/cicd-flask-app.git'
            }
        }
        stage('Install Dependencies') {
            steps {
                sh '''
                pip3 install -r requirements.txt
                '''
            }
        }
        stage('Deploy') {
            steps {
                sh '''
                # Kill old app if running
                pkill -f "python3 app.py" || true

                # Copy app files to /var/www
                cp -r ./* /var/www/flaskapp/

                # Run app in background
                nohup python3 /var/www/flaskapp/app.py > /var/www/flaskapp/app.log 2>&1 &
                '''
            }
        }
    }
}
