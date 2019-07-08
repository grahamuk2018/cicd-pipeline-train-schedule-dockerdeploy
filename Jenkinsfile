pipeline {
  agent none
  stages {
    stage('Build Packer Container') {
      agent {
        any
      }
      steps {
        script {
          packer = docker.build("grahamseanking/packer")
        }
      }
    }
    stage("Push Docker Image") {
      steps {
        agent {
          any
        }
      }
    }
    script {
      docker.withRegistry("195027210696.dkr.ecr.eu-west-1.amazonaws.com/grahamseanking/packer") {
        packer.push("latest")
      }
    }
    stage("Create Base AMI") {
      agent {
        docker {
          image grahamseanking/packer
        }
      }
      steps {
        sh "packer build paker.json"
      }
    }
  }
}
