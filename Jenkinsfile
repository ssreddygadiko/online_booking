pipeline {
  environment {
    registry = '675274863130.dkr.ecr.ap-south-1.amazonaws.com/test'
    registryCredential = 'dfba16958617d3ba643003ec707cfc1e6da6dd80'
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
