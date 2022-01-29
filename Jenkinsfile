node('jdk11-mvn3.8.4') {
    stage('git') {
       git branch: 'main', url: 'https://github.com/Madanalaanand/spring-petclinic.git'
  }
    stage('build') {
       sh 'mvn clean package'
}
}