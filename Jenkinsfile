
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
        stage('Deploy Docker Container') { 
            steps {
                sh '/home/ec2-user/spring-boot-monitoring-sample-master/docker-compose up' 
            }
        }
    }
}
