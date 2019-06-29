#!/bin/env groovy
pipeline {
node {  
    stage('Clone sources') {
        git url: 'https://github.com/devopsroman/oms.git'
    }
    stage ('Build OMS') {
        sh 'mvn clean install'
    }
}
}
