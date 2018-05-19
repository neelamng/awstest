pipeline {
  agent {
    node {
      label 'redhat-agent'
    }

  }
  stages {
    stage('install packer') {
      steps {
        sh '''sudo yum install unzip -y
curl -o packer.zip https://releases.hashicorp.com/packer/1.1.3/packer_1.1.3_linux_amd64.zip?_ga=2.25536829.1444204868.1515428339-1209176675.1503914009
/usr/bin/unzip -o packer.zip
./packer validate packer.json'''
      }
    }
    stage('Build AMI') {
      steps {
        sh '''./packer build packer.json
'''
        sh '''ami=$(grep artifact manifest.json | tail -1 | awk -F\':\' \'{print $3}\' | sed \'s/\\",//g\')
echo $ami'''
        sh 'aws cloudformation create-stack --stack-name myteststack --template-body file://ec2-testwork.yml --parameters ParameterKey=AMIID,ParameterValue=${ami} --capabilities CAPABILITY_IAM --region us-east-1'
      }
    }
    stage('archive output') {
      steps {
        archiveArtifacts 'output.txt'
      }
    }
  }
}