pipeline {
    agent { label 'jdk11-mvn3.8.4' }
    triggers { 
        cron('45 23 * * 1-5')
        pollSCM('*/5 * * * *')
    }
	tools {
		maven 'MVN_3.8.4'
	}
    stages {
        stage('scm') {
            steps {
                git url: 'https://github.com/Madanalaanand/spring-petclinic.git', branch: 'jfrog'
            }
        }
        stage ('Artifactory configuration') {
            steps {
                rtMavenDeployer (
                    id: "MAVEN_DEPLOYER",
                    serverId: 'JFROG-OSS',
                    releaseRepo: 'local-relesaes',
                    snapshotRepo: 'local-snapshort'
                )
                
            }
        }
        stage ('Exec Maven') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'JFROG_ARTIFACTORY', usernameVariable: 'ARTIFACTORY_USERNAME', passwordVariable: 'ARTIFACTORY_PASSWORD')]) {
                    rtMavenRun (
                        tool: 'MVN_3.8.4', 
                        pom: 'pom.xml',
                        goals: 'clean install',
                        deployerId: "MAVEN_DEPLOYER"
                    )
                }
            }
        }
        stage ('Publish build info') {
            steps {
                rtPublishBuildInfo (
                    serverId: 'JFROG-OSS'
                )
            }
        }
    }
}