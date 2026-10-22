pipeline {
    agent any

    stages {

        stage('Build') {
            steps {
                sh 'docker build -t flask-jenkins-app:1.0 .'
            }
        }

        stage('Deploy') {
            steps {
                sh '''
                    docker rm -f flask-jenkins-app || true

                    docker run -d \
                        --name flask-jenkins-app \
                        -p 5000:5000 \
                        flask-jenkins-app:1.0
                '''
            }
        }

        stage('Test') {
            steps {
                sh 'curl -f http://localhost:5000/health'
            }
        }
    }

    post {
        success {
            echo 'Flask application deployed successfully!'
        }

        failure {
            echo 'Pipeline failed. Check the Console Output.'
        }
    }
}
