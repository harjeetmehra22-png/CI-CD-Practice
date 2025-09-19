pipeline {
  agent any

  stages {
    stage('Checkout') {
      steps {
        checkout scm
      }
    }

    stage('Build Docker Image') {
      steps {
        sh 'docker build -t dockerized-ci-cd:latest .'
      }
    }

    stage('Run Container') {
      steps {
        sh 'docker run --rm dockerized-ci-cd:latest'
      }
    }
  }
}
