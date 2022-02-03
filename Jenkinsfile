pipeline{
   agent{'jdk11-maven3.8.4'}
   stages{
      stage('scm'){
         steps{
            git 'https://github.com/Madanalaanand/spring-petclinic.git', branch 'main'
         }
      }
      stage('build'){
         steps{
            sh '/usr/local/apache-maven3.8.4/bin/mvn clean package'
         }
      }
   }
   post{
      always{
         mail to: 'madanalaanand7@gmail.com',
         from: 'team@gmail.com',
         subject: "status of the pipeline ${currentBuild.fullDisplayName}",
         body: "${env.BUILD_URL}" has "${currentBuild.result}"
      }
   }
}