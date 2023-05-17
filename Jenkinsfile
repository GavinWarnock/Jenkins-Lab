pipeline {
  agent any
  stages {
    stage('Test') {
      steps {
        sh 'echo "Running tests..."'
        script {
          def nodejsTool = tool name: 'node-20-tool', type: 'jenkins.plugins.nodejs.tools.NodeJSInstallation'
          env.PATH = "${nodejsTool}/bin:${env.PATH}"
        }
        sh "node --version"
      }
    }
    stage('Build') {
      steps {
        sh 'echo "Building application..."'
      }
    }
    stage('Docker') {
      steps {
        sh 'echo "Building image and pushing to Docker Hub..."'
        script {
          def dockerTool = tool name: 'docker-latest-tool', type: 'otg.jenkinsci.plugins.docker.commons.tools.DockerTool'
          env.PATH = "${dockerTool}/bin:${env.PATH}"
        }
        withCredentials([usernamePassword(credentialsId: 'personal-docker-credentials', usernameVariable: 'DOCKER_USERNAME', passwordVariable: 'DCOKER_PASSWORD')]) {
          sh "echo ${DOCKER_USERNAME}"
        }
        sh "docker --version"
      }
    }
    stage('Deploy') {
      steps {
        sh 'echo "Deploying application to EC2 instance..."'
      }
    }
  }
}
