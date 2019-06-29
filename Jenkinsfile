node {
try {  
    stage('Clone sources') {
        git url: 'https://github.com/devopsroman/oms.git'
    }
    stage ('Build OMS') {
        sh 'mvn clean install'
    }
}
}
