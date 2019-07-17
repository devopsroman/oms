node('standalone-linux-slave1') {
  stage('Git clone') {
    git 'https://github.com/devopsroman/oms.git'
} 
  stage('Build docker images') {
     //sh "mvn sonar:sonar"
} 
  stage('SonarQube analysis') {
    sh "mvn sonar:sonar"
} 
  stage('Build & Test') {
    def mvnHome = tool 'M3'
    sh "${mvnHome}/bin/mvn -B -Dmaven.test.failure.ignore verify"
}
  stage('Archiving artifacts') {
    step([$class: 'ArtifactArchiver', artifacts: '**/target/*.war', fingerprint: true])
}
  stage('Uploading artifact to Nexus') {
    nexusArtifactUploader artifacts: [[artifactId: 'maven-deploy-plugin', classifier: '', file: '/home/jenkins/workspace/oms_lv419/target/OMS.war', type: 'war']], credentialsId: 'nexus', groupId: 'org.apache.maven.plugins', nexusUrl: '10.26.34.246:8081', nexusVersion: 'nexus3', protocol: 'http', repository: 'test1', version: '5.7.112'
}
  stage('Deploy to stage') {
    sshagent(['ssh_tomcat']) {
    sh 'scp -r target/OMS.war root@10.26.34.145:/opt/tomcat/webapps'
}}}
