pipeline {
  environment {
    registry = '675274863130.dkr.ecr.ap-south-1.amazonaws.com/test'
    registryCredential = '9d0d63cca5028f996fdf3db7ca736666e6422d46'
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
