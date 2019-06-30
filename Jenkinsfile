node('centos') {  
    stage('Clone sources') {
        git url: 'https://github.com/devopsroman/oms.git'
    }
    stage ('Build OMS') {
        sh 'mvn clean install'
    }
    stage ('SonarQube Analysys') {
        def scannerHome = tool 'SonarQube Scanner 2.8';
        withSonarQubeEnv('My SonarQube Server') {
          sh "${scannerHome}/bin/sonar-scanner"
          }
    }
}
