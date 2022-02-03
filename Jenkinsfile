pipeline{
   agent{label 'jdk11-mvn3.8.4'}
   stages{
      stage('scm'){
         steps{
            git url: "https://github.com/Madanalaanand/spring-petclinic.git", branch: "main"
         }
      }
      stage('build'){
         steps{
                mail from: 'madanalaanand7@gmail.com',
                to : 'anand@gmail.com',
                subject: "status of the pipeline ${currentBuild.fullDisplayName}",
                body: "${env.BUILD_URL} has a result ${currentBuild.result}"
                withSonarQubeEnv(installationName: 'SONAR_9.3', envOnly: true, credentialsId: 'SONAR_TOKEN'){
                sh '/usr/local/apache-maven-3.8.4/bin/mvn clean package sonar:sonar'
                 echo "${env.SONAR_HOST_URL}"
    
                } 
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