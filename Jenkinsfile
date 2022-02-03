pipeline{
   agent{label 'jdk11-mvn3.8.4'}
   stages{
      stage('scm'){
         steps{
            git url: 'https://github.com/Madanalaanand/spring-petclinic.git', branch: "main"
         }
      }
      stage('build'){
         steps{
                sh '/usr/local/apache-maven-3.8.4/bin/mvn clean package'
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