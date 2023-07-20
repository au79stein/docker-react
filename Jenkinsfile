pipeline {
  agent any
  stages {
    stage("verify tooling") {
      steps {
        sh '''
          docker version
          docker info
          docker compose version
          curl --version
          jq --version
        '''
      }
    }
    // clean up all docker files that are there
    stage('Prune Docker data') {
      steps {
        sh 'docker system prune -a --volumes -f'
      }
    }
    stage('Build image') {
      steps {
        container('builder') {
          script {
            sh "docker build -t yessrerich/docker-react -f Dockerfile.dev ."
          }
        }
      }
    }
  }
}
