node {
   def mvnHome
   stage('Preparation') { // for display purposes
      // Get some code from a GitHub repository
      git 'https://github.com/kishoregaws/cicd.git'
      // Get the Maven tool.
      // ** NOTE: This 'M3' Maven tool must be configured
      // **       in the global configuration.           
      mvnHome = tool 'M2_HOME'
   }
   stage('Build') {
      // Run the maven build
      withEnv(["M2_HOME=$mvnHome"]) {
         if (isUnix()) {
            sh '"$M2_HOME/bin/mvn" -Dmaven.test.failure.ignore clean package'
         } else {
            bat(/"%MVN_HOME%\bin\mvn" -Dmaven.test.failure.ignore clean package/)
         }
      }
   }
   stage('Results') {
      archiveArtifacts 'target/*.jar'
   }
}
