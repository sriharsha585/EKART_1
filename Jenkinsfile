pipeline {
  agent any
  tools {
    maven 'Maven'
    jdk 'Java11'
  }
  stages {
    stage('Checkout') {
      steps {
        git branch: 'main', url: 'https://github.com/sriharsha585/EKART_1.git'
      }
    }
    stage('Build') {
      steps {
        sh 'mvn clean package'
      }
    }
    stage('sonarqube Analysis') {
      steps {
        withSonarQubeEnv('SonarQube') {
          sh 'mvn sonar:sonar -Dsonar.projectKey=Ekart'
        }
      }
    }
    stage('Build Docker Image') {
          steps {
            sh 'docker build -t ekart:latest .'
          }
          }
    stage('Run container') {
      steps {
        sh 'docker run -d --name ekart -p 8070:8070 ekart:latest'

      }
    }
          }
          }
