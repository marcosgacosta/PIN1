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
        sh "docker run -d -rm -p 3000:3000 testapp npm test"
      }
    }
   stage('Deploy Image') {
      steps{
        sh '''
        docker login -u admin -p hola1234 localhost:8083
        docker tag testapp localhost:8083/repository/marcosdocker/testapp:latest
        docker push localhost:8083/repository/marcosdocker/testapp:latest
        '''
        }
      }
    }
}


    
  

