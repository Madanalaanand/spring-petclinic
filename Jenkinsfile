pipeline{
   agent{label 'jdk11-maven3.8.4'}
   stages{
      stage('scm'){
         steps{
            git url: "https://github.com/Madanalaanand/spring-petclinic.git", branch: "main"
         }
      }
      stage('build'){
         steps{
            sh "/usr/local/apache-maven3.8.4/bin/mvn clean package"
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