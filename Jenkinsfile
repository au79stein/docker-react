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
        script {
          //sh 'docker build -t yessrerich/docker-react -f Dockerfile.dev .'
          sh 'docker build -t au79stein/docker-react -f Dockerfile.dev .'
        }
      }
    }
    stage('Testing') {
      steps {
        script {
          // tag is used internally only doesn't matter what you call it really
          //sh 'docker run yessrerich/docker-react npm run test -- --coverage'
          //sh 'docker run au79stein/docker-react npm run test -- --coverage'
          sh 'docker run -e CI=true au79stein/docker-react npm run test -- --coverage'
        }
      }
    }
  }
}
