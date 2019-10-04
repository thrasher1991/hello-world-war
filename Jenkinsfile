node {
   def mvnHome
   stage('Preparation') { // for display purposes
      // Get some code from a GitHub repository
      git 'https://github.com/thrasher1991/hello-world-war.git'
      // Get the Maven tool.
      // ** NOTE: This 'M3' Maven tool must be configured
      // **       in the global configuration.           
      mvnHome = tool 'MVN_HOME'
   }
   stage('Build') {
        git 'https://github.com/thrasher1991/hello-world-war.git'
      // Run the maven build
      withEnv(["MVN_HOME=$mvnHome"]) {
         if (isUnix()) {
            sh '"$MVN_HOME/bin/mvn" -Dmaven.test.failure.ignore clean package'
         } else {
            bat(/"%MVN_HOME%\bin\mvn" -Dmaven.test.failure.ignore clean package/)
         }
      }
   }

   stage('Deploy to Tomcat')
   {
    withEnv(["MVN_HOME=$mvnHome"]) {
         
  
   deploy adapters: [tomcat9(credentialsId: 'tomcat', path: '', url: 'http://18.220.194.35')], contextPath: 'hello-world.war', war: '**/*.war'
   
   
   }
   
   }
          stage('Deploy to Nexus') {
      // Run the maven build
      withEnv(["MVN_HOME=$mvnHome"]) {
         if (isUnix()) {
            sh '"$MVN_HOME/bin/mvn" -Dmaven.test.failure.ignore clean deploy'
         } else {
            bat(/"%MVN_HOME%\bin\mvn" -Dmaven.test.failure.ignore clean deploy/)
         }
      }
   }

   
}
