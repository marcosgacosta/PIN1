pipeline {
  agent {
         label 'docker'
    }

  options {
    timeout(time: 2, unit: 'MINUTES')
  }

  environment {
    ARTIFACT_ID = "elbuo8/webapp:${env.BUILD_NUMBER}"
  }
   stages {
   stage('Building image') {
      steps{
          sh '''
          docker build -t testapp .
             '''  
        }
    }
  
  
    stage('Run tests') {
      steps {
        sh "docker run testapp npm test"
      }
    }
   stage('Deploy Image') {
      steps{
        sh '''
        docker tag testapp 10.0.0.101:8081/repository/marcosdocker/:test
        docker push 10.0.0.101:5000/repository/marcosdocker/:test
        '''
        }
      }
    }
}


    
  

