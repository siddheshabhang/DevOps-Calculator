pipeline {
    agent any
  
    stages {
        stage('Checkout Repo') {
            steps {
                git 'https://github.com/siddheshabhang/DevOps-Calculator.git'
            }
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
        stage('Docker Build') {
            steps {
                sh 'docker build -t siddheshhh/calculator-app:1.0 .'
            }
        }
    }
}
