pipeline {
    agent { label 'master' }

options {
        skipStagesAfterUnstable()
    }
    stages {
        stage('Build Spring-boot') {
            steps {
                sh 'mvn -B -DskipTests clean package'
            }
        }

        stage('Deploy Docker Container Apps') { 
            steps {
                sh 'cd /var/lib/jenkins/apps/spring-boot-monitoring-sample-master'
                sh '/usr/local/bin/docker-compose up -d'
            }
        }
        
        stage('Push Docker to ECR') {
            steps {
                
                sh 'docker push 031440218568.dkr.ecr.us-east-1.amazonaws.com/fampoc:latest'
            }
        }
    }
}
