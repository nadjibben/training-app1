node {
   def mvnHome
   stage('Preparation') { // for display purposes
      // Get some code from a GitHub repository
      git 'https://github.com/nadjibben/training-app1.git'
      // Get the Maven tool.
      // ** NOTE: This 'M3' Maven tool must be configured
      // **       in the global configuration.           
      mvnHome = tool 'maven3'
   }
   stage('Test') {
      if (isUnix()) {
         sh "${mvnHome}/bin/mvn' test"
      } else {
      bat(/"${mvnHome}\bin\mvn" test/)
      }
   }
   stage('Results') {
      junit '**/target/surefire-reports/TEST-*.xml'
      archiveArtifacts 'target/*.jar'
   }
    stage('Execute Jar') {
      if (isUnix()) {
         sh "'$java -jar target/*.jar"
      } else {
         bat(/java -jar target\/training-app-1.0-jar-with-dependencies.jar/)
        }
    }
    stage('Publish Artefact') {
      if (isUnix()) {
         sh "${mvnHome}/bin/mvn' -DdeployOnly deploy"
      } else {
      bat(/"${mvnHome}\bin\mvn" -DdeployOnly deploy -s "C:\apache-maven-3.6.0\conf\settings.xml"/)
      }
    }
}
