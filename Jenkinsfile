pipeline {
  agent any

  stages {

    stage('Build And Push Container Image') {
      steps {
        withCredentials([usernamePassword(credentialsId: 'docker-credentials', usernameVariable: 'DOCKER_USERNAME', passwordVariable: 'DOCKER_PASSWORD')]) {
            sh "mvn clean package jib:build"
        }
      } 
    }
    
  stage('Deploy to K8s') {
      steps {
        script {
          kubernetesDeploy(configs: "k8s.yaml", kubeconfigId: "kubeconfig-credentials")
        }
      } 
    }
  }
}