pipeline {
    agent any

    environment {
        APP_ENV = 'dev'
    }

    stages {
        stage('Checkout') {
            steps { checkout scm }
        }

        stage('Build') {
            steps {
                sh 'mvn clean package'  
            }
        }

        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }

        stage('Deploy') {
            steps {
                echo "Deploying to ${env.APP_ENV} environment..."
            }
        }
    }
}
