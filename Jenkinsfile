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
      mvn clean verify sonartool name: 'Sonar3', type: 'hudson.plugins.sonar.SonarRunnerInstallation':sonar 
}
  
  stage('Maven') {
    def mvnHome = tool 'M3'
    sh "${mvnHome}/bin/mvn -B -Dmaven.test.failure.ignore verify"
} 
  
  stage('Artifact') {
    step([$class: 'ArtifactArchiver', artifacts: '**/target/*.war', fingerprint: true])
}

}
