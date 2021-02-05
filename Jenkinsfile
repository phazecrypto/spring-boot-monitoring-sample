
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
                sh 'sudo /home/ec2-user/spring-boot-monitoring-sample-master/docker-compose up' 
            }
        }
    }
}
