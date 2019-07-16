node('docker-maven-build-slave1'') {
  stage('Clone') {
    checkout scm: [$class: 'GitSCM', branches: [[name: '*/master']], userRemoteConfigs: [[url: 'https://github.com/devopsroman/oms.git']]]
} 
  stage('Maven') {
  def mvnHome = tool 'M3'
  sh "${mvnHome}/bin/mvn -B -Dmaven.test.failure.ignore verify"
} 
  
  stage('Artifact') {
    step([$class: 'ArtifactArchiver', artifacts: '**/target/*.war', fingerprint: true])
}

}
