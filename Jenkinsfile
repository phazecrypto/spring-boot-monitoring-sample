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
            def notify(status) {
       wrap([$class: 'BuildUser']) {
       emailext (
       subject: "${status}: Job ${env.JOB_NAME} ([${env.BUILD_NUMBER})",
       body: """
       Check console output at <a href="${env.BUILD_URL}">${env.JOB_NAME} (${env.BUILD_NUMBER})</a>""",
       to: "${BUILD_USER_EMAIL}",
       from: 'jenkins@company.com')
   }
}
        }
    }
}
