pipeline {
agent any
stages {

    stage('Install Dependencies') {
        steps {
            sh '''
                python3 -m venv venv

                ./venv/bin/python -m pip install --upgrade pip

                ./venv/bin/pip install Django==5.1.2
                ./venv/bin/pip install scikit-learn
                ./venv/bin/pip install pandas
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
    stage('Test') { 
        steps { 
            sh './venv/bin/python manage.py test' 
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
        echo 'Build and tests passed successfully!'
    }

    failure {
        echo 'Build or tests failed!'
    }
}

}
