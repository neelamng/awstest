pipeline {
  agent any
  stages {
    stage('Validate packer') {
      steps {
        bat(script: 'C:/packer.exe validate packer.json', returnStatus: true, returnStdout: true)
      }
    }
    stage('Build AMI') {
      steps {
        bat(script: 'C:/packer.exe build packer.json', returnStatus: true, returnStdout: true)
      }
    }
  }
}