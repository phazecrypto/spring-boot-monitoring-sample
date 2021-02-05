
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
                sh 'aws ecr get-login-password --region us-east-1 | docker login --username jenkins --password-stdin 031440218568.dkr.ecr.us-east-1.amazonaws.com'
                sh 'cd /var/lib/jenkins/apps/spring-boot-monitoring-sample-master'
                sh 'docker-compose up' 
            }
        }
    }
}
