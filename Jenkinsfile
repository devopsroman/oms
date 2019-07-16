node('docker-maven-build-slave1') {
  
  stage('Preparation') { 
      // for display purposes
      // Get some code from a GitLub repository
     checkout scm: [$class: 'GitSCM', branches: [[name: '*/master']], userRemoteConfigs: [[url: 'https://github.com/devopsroman/oms.git']]];
      // Get the Maven tool.
      // ** NOTE: This 'maven-demo' Maven tool must be configured
      // **       in the global configuration.      
} 
  stage('SonarQube') {
      tool name: 'Sonar3', type: 'hudson.plugins.sonar.SonarRunnerInstallation'
}
  
  stage('SonarQube analysis') {
    withSonarQubeEnv('my-sonarqube-demo') {
    sh "'${mvnHome}/bin/mvn' sonar:sonar"
             // If SonarQube require authentication and token absent in Global Jenkins configuration
            //sh "'${mvnHome}/bin/mvn' sonar:sonar -Dsonar.login=token_value"
     	
}
  
  stage('Maven') {
    def mvnHome = tool 'M3'
    sh "${mvnHome}/bin/mvn -B -Dmaven.test.failure.ignore verify"
} 
  
  stage('Artifact') {
    step([$class: 'ArtifactArchiver', artifacts: '**/target/*.war', fingerprint: true])
}

}
