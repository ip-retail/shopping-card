node('maven-label') {
   def mvnHome
   stage('Preparation') { 
      
      git 'https://github.com/ip-retail/shopping-card.git'
              
      mvnHome = tool 'maven'
   }
   stage('Build') {
    
      withEnv(["MVN_HOME=$mvnHome"]) {
         if (isUnix()) {
            sh '"$MVN_HOME/bin/mvn" -Dmaven.test.failure.ignore clean deploy'
         } else {
            bat(/"%MVN_HOME%\bin\mvn" -Dmaven.test.failure.ignore clean package/)
         }
      }
   }
   stage('Results') {
      junit '**/target/surefire-reports/TEST-*.xml'
      archiveArtifacts 'target/*.jar'
   }
}
