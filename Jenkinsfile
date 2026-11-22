pipeline{
  //agent{
  //   docker { image 'node:22-alpine'} 
  //}
  agent {
        docker { image 'node:18-alpine' }
  }

  options{
    disableConcurrentBuilds()
  }

  //triggers{
  //  pollSCM('H/5 * * * *')
  //}

  stages{
    stage ('Build Backend'){
      steps{
        dir('backend'){
            sh 'npm ci'
            sh 'npm run check'
        }
        
      }
    }

    stage ('Build Frontend'){
      steps {
          dir('frontend'){
            sh 'npm ci'
            sh 'npm run build'
          }
      }
    }

    stage('Test Backend'){

      steps{
          dir('backend'){
            sh 'npm test'
          }
      }
    }

    stage('Test Frontend'){
      environment{
          CI= 'true'
      }
      steps{
        
        dir('frontend'){
          sh 'npm test'
        }
      }
    }
  }

  post {
        success {
            archiveArtifacts artifacts: 'frontend/build/**', fingerprint: true
        }
        failure {
            echo 'The pipeline failed. Read the console output above.'
        }
        always {
            cleanWs()
        }
  }
}
