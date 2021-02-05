
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
        
        stage('Docker Login') {
            steps {
                sh 'aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin 031440218568.dkr.ecr.us-east-1.amazonaws.com'
            }
        }
        stage('Deploy Docker Container') { 
            steps {
                sh '/home/ec2-user/spring-boot-monitoring-sample-master/docker-compose up' 
            }
        }
    }
}
