pipeline {
    
    agent any
    
    environment {
        registry = "919381825954.dkr.ecr.us-east-2.amazonaws.com/test-python-flask-app"
    }
    stages {
        
        stage ('scm checkout') {
            steps {
            
               checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/betrand2470/GA-flask-app']])
            }
        } 
        
        stage ('Docker Build') {
            steps {
                script {
                    dockerImage = docker.build registry
                }
            }
        }
        
        stage ('Docker Push to ECR') {
            steps {
                sh 'aws ecr get-login-password --region us-east-2 | docker login --username AWS --password-stdin 919381825954.dkr.ecr.us-east-2.amazonaws.com'
                sh 'docker push 919381825954.dkr.ecr.us-east-2.amazonaws.com/test-python-flask-app:latest'
            }
        }
        
    }
    
}