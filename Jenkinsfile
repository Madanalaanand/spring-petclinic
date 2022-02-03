pipeline{
   agent{label 'jdk11-mvn3.8.4'}
   tools {
		maven 'MVN_3.8.4'
	}
   stages{
      stage('scm'){
         steps{
            git url: "https://github.com/Madanalaanand/spring-petclinic.git", branch: "main"
         }
      }
      stage ('Artifactory configuration') {
            steps {
                rtMavenDeployer (
                    id: "MAVEN_DEPLOYER",
                    serverId: "JFROG-OSS",
                    releaseRepo: local-relesaes,
                    snapshotRepo: local-snapshort
                )
            }
        }
         stage ('Exec Maven') {
            steps {
                rtMavenRun (
                    tool: 'MVN_3.8.4', // Tool name from Jenkins configuration
                    pom: 'pom.xml',
                    goals: 'clean install',
                    deployerId: "MAVEN_DEPLOYER"
                )
            }
        }
        stage ('Publish build info') {
            steps {
                rtPublishBuildInfo (
                    serverId: "JFROG-OSS"
                )
            }
        }
   }
    post{
            always{
                mail from: 'madanalaanand7@gmail.com',
                to : 'anand@gmail.com',
                subject: "status of the pipeline ${currentBuild.fullDisplayName}",
                body: "${env.BUILD_URL} has a result ${currentBuild.result}"

            }
        }
}