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
        bat(script: 'C:/packer.exe build packer.json > output.txt', returnStatus: true, returnStdout: true)
      }
    }
    stage('deploy cloudformation') {
      steps {
        bat(script: 'aws cloudformation create-stack --stack-name stacknew --template-body file://C:/aws/ec2-testwork.yml', returnStatus: true, returnStdout: true)
      }
    }
    stage('archive output') {
      steps {
        archiveArtifacts 'output.txt'
      }
    }
  }
  environment {
    AWS_SHARED_CREDENTIALS_FILE = 'C:\\Users\\nagaraj\\.aws\\credentials'
  }
}