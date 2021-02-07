pipeline {
    agent { label 'master' }

options {
        skipStagesAfterUnstable()
    }
    stages {
        stage('Build') {
            steps {
                sh 'mvn -B -DskipTests clean package'
            }
        }

        stage('Deploy Docker') { 
            steps {
                sh 'cd /var/lib/jenkins/apps/spring-boot-monitoring-sample-master'
                sh '/usr/local/bin/docker-compose up -d'
            }
        }
        
        stage('Push Docker to ECR') {
            steps {
                sh 'aws ecr get-login-password --region us-east-1 --profile=default | docker login --username AWS --password-stdin 031440218568.dkr.ecr.us-east-1.amazonaws.com'
                sh 'docker push 031440218568.dkr.ecr.us-east-1.amazonaws.com/fampoc:latest'
            }
        }
    }
}
