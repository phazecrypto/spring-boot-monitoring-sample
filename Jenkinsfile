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
        stage('Email Notification'){
            emailext (
            subject: "Job '${env.JOB_NAME} ${env.BUILD_NUMBER}'",
            body: """<p>Check console output at <a href="${env.BUILD_URL}">${env.JOB_NAME}</a></p>""",
            to: "phazecrypto@gmx.com",
            from: "jenkins@runjob.org")
        }
    }
}
