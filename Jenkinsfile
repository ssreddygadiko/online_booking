pipeline {
  environment {
    registry = '675274863130.dkr.ecr.ap-south-1.amazonaws.com/test'
    registryCredential = '51cb1bd0cadbf02d47662b78138a9bd785144ca7'
    dockerImage = ''
  }
  agent any
  stages {
    stage('Building image') {
      steps{
        script {
          dockerImage = docker.build registry + ":$BUILD_NUMBER"
        }
      }
    }
    stage('Deploy image') {
        steps{
            script{
                docker.withRegistry("https://" + registry, "ecr:ap-south-1:" + registryCredential) {
                    dockerImage.push()
                }
            }
        }
    }
  }
}
