pipeline {
    agent {
        label 'uta-attendance-app'
    }

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build Environment') {
            steps {
                sh '''
                    python3 --version
                    python3 -m venv .venv
                    . .venv/bin/activate
                    pip install --upgrade pip
                    pip install -r requirements.txt
                '''
            }
        }

        stage('Lint') {
            steps {
                sh '''
                    . .venv/bin/activate
                    python3 -m py_compile app.py
                '''
            }
        }

        stage('Test') {
            steps {
                sh '''
                    . .venv/bin/activate
                    pytest -q
                '''
            }
        }

        stage('Package') {
            steps {
                sh '''
                    mkdir -p build
                    tar -czf build/uta-attendance-${BUILD_NUMBER}.tar.gz \
                        app.py \
                        requirements.txt \
                        templates \
                        static \
                        tests
                '''
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deployment stage will be configured next.'
            }
        }

        stage('Verify') {
            steps {
                echo 'Verification stage will be configured next.'
            }
        }
    }

    post {
        success {
            echo "UTA Attendance pipeline completed successfully."
        }
        failure {
            echo "UTA Attendance pipeline failed."
        }
    }
}
