pipeline {
  agent any

  environment {
    APP_ENV = 'dev'
  }

  tools {
    jdk 'jdk11'       // name configured in Jenkins Global Tool Config
    maven 'Maven3'    // name configured in Jenkins Global Tool Config
  }

  parameters {
    string(name: 'BRANCH', defaultValue: 'main', description: 'Branch to build')
  }

  stages {
    stage('Checkout') {
      steps { checkout scm }
    }

    stage('Build') {
      steps {
        sh 'mvn -B clean package'
      }
    }

    stage('Test') {
      steps {
        sh 'mvn test'
        junit 'target/surefire-reports/*.xml'
      }
    }

    stage('Archive') {
      steps {
        archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
      }
    }

    stage('Deploy') {
      steps {
        echo "Deploying to ${params.BRANCH} / ${env.APP_ENV}"
        // example: scp/ssh deploy using credentials via sshagent
      }
    }
  }

  post {
    success { echo 'Pipeline completed successfully.' }
    failure { echo 'Pipeline failed.' }
  }
}
