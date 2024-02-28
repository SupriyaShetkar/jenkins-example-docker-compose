pipeline {
  agent {
        label 'docker_000140'
  }
  stages {
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
    stage('Push image to Docker Hub') {
            steps {
                script {
                    docker.withRegistry('https://registry.hub.docker.com', 'dockerhub-jenkins') {
                        docker.image('website1:v2').push('latest')
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
