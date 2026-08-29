```groovy
pipeline {
    agent any

    stages {

        stage('Install Dependencies') {
            steps {
                sh '''
                    python3 -m venv venv
                    ./venv/bin/python -m pip install --upgrade pip
                    ./venv/bin/pip install Django==5.1.2
                '''
            }
        }

        stage('Django Check') {
            steps {
                sh '''
                    ./venv/bin/python manage.py check
                '''
            }
        }

        stage('Collect Static') {
            steps {
                sh '''
                    ./venv/bin/python manage.py collectstatic --noinput
                '''
            }
        }
    }

    post {
        success {
            echo 'Build successful!'
        }

        failure {
            echo 'Build failed!'
        }
    }
}
```
