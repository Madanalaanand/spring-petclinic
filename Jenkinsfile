pipeline {
    agent { label 'jdk11-mvn3.8.4' }
    triggers { 
        cron('45 23 * * 1-5')
        pollSCM('*/5 * * * *')
    }
    stages {
        stage('scm') {
            steps {
               
                git url: 'https://github.com/GitPracticeRepo/spring-petclinic.git', branch: 'main'
            }
        }
        stage('build') {
            steps {
                withSonarQubeEnv(installationName: 'SONAR_9.2.1') {
                    sh "mvn clean package sonar:sonar"                                  
                }
            }
        }
    }
}