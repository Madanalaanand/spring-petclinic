pipeline{
   agent('jdk11-maven3.8.4'){
      stages{
         stage{
            steps('scm'){
              git 'https://github.com/Madanalaanand/spring-petclinic.git', branch 'main'
            }
         }
         stage{
            steps('build'){
               sh '/usr/local/apache-maven-3.8.4/bin/mvn clean package'
            }
         }
      }
   }
   post{
      always{
         mail to: 'madanalaanand7@gmail.com',
         from: 'team@gmail.com',
         subject: "status of the pipeline.${currentBuild.fullDisplayName}",
         body: "${env.Build_URL} is ${currentBuild.result}"
      }
   }
}