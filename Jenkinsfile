pipeline {
  agent {
        label 'docker_000140'
  }
 
    stage("verify tooling") {
      steps {
        sh '''
          docker version
          docker info 
        '''
      }
    }
  
    stage('Start container') {
      steps {
        sh 'docker-compose up -d'
        sh 'docker-compose ps'
      }
    }
    stage('Run tests against the container') {
      steps {
        sh 'curl http://localhost:8082/index.html'
      }
    }
   
  }
  }
  post {
    always {
      sh 'docker-compose down'
      sh 'docker-compose ps'
    }
  }
}
