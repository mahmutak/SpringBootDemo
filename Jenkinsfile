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
      withKubeConfig([credentialsId: 'kubeconfig-credential2']) {
        sh 'kubectl apply -f  k8s.yaml'
      }
    }
    }
  }
}

/*mkdir -p /home/jenkins/k8s/certs
cp ~/.minikube/ca.crt /home/jenkins/k8s/certs
cp /root/.minikube/profiles/minikube/client.* /home/jenkins/k8s/certs/
chown -R jenkins:jenkins /home/jenkins/k8s/certs*/