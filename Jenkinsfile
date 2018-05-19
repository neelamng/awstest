pipeline {
  agent {
    node {
      label 'redhat-agent'
    }

  }
  stages {
    stage('install packer') {
      steps {
        sh '''curl -o packer.zip https://releases.hashicorp.com/packer/1.1.3/packer_1.1.3_linux_amd64.zip?_ga=2.25536829.1444204868.1515428339-1209176675.1503914009
unzip -o packer.zip
./packer validate packer.json'''
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
}