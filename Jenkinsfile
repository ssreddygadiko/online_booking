pipeline {
  environment {
    registry = '675274863130.dkr.ecr.ap-south-1.amazonaws.com/test'
    registryCredential = 'e8430fccf6a705a482345c84a76ee56bb624a79b'
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
