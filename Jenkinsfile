pipeline {
    agent any
  
    stages {
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
        stage('Docker Build & Tag') {
            steps {
                sh 'docker build -t calculator-app:1.0 .'
                sh 'docker tag calculator-app:1.0 siddheshhh/calculator-app:1.0'
            }
        }
        stage('Docker Push') {
            steps {
                withCredentials([usernamePassword(
                        credentialsId: 'dockerhub-creds',
                        usernameVariable: 'DOCKER_USER',
                        passwordVariable: 'DOCKER_PASS')]) {
                    sh '''
                        echo $DOCKER_PASS | docker login -u $DOCKER_USER --password-stdin
                        docker push siddheshhh/calculator-app:1.0
                    '''
                }
            }
        }
    }
    post {
        success {
            mail to: 'siddhesh.ghanasham@iiitb.ac.in',
                 subject: "Build Success",
                 body: "Calculator build succeeded!"
        }
    
        failure {
            mail to: 'siddhesh.ghanasham@iiitb.ac.in',
                 subject: "Build Failed",
                 body: "Build failed. Check Jenkins."
        }
    }
}
