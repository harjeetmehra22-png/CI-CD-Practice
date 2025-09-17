pipeline {
  agent any

  stages {
    stage('Checkout') {
      steps { checkout scm }
    }

    stage('Build Docker image') {
      steps {
        script {
          sh 'docker build -t dockerized-app:${BUILD_NUMBER} .'
        }
      }
    }

    stage('Run container and capture output') {
      steps {
        script {
          sh 'docker run --rm dockerized-app:${BUILD_NUMBER} > output.txt || true'
          sh 'echo "=== Container output ==="'
          sh 'cat output.txt || true'
        }
      }
    }
  }

  post {
    always {
      archiveArtifacts artifacts: 'output.txt', fingerprint: true
      sh 'docker rmi dockerized-app:${BUILD_NUMBER} || true'
    }
  }
}
