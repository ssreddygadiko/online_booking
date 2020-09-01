pipeline {
  environment {
    registry = '675274863130.dkr.ecr.ap-south-1.amazonaws.com/test'
    registryCredential = 'e97005edc62c444171614cc238c52e5346e17112'
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
