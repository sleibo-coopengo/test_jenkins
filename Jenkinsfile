pipeline {
  agent any
  environment {
    def TAG = get_tag()
  }

  triggers {
    cron('H 00 * * *')
  }

  stages {
    stage('Test coog image') {
      steps {
        script {
        sh '''
            echo test stage 1
            '''
        }
      }
    }
    stage('Coucou') {
      steps {
        script {
        sh '''
            echo test stage 2
            '''
        }
      }
    }
  }

  post {
    success {
      script {
        sh '''
            echo success
        '''
        }
    }
    failure {
      script {
        sh '''
            echo Failure
        '''
        }
    }
    unstable {
      script {
        sh '''
            echo Unstable
        '''
        }
    }
  }

}
def get_tag() {
    node('master') {
        return env.ref.split('/')[-1]
    }
}
