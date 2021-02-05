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
    }
}
