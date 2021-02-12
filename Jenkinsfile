pipeline {

  agent {
    docker {
        image 'alpine-linux'
    }
  }

  environment {
    def TAG = get_tag()
  }

  triggers {
    cron('H 00 * * *')
  }

  stages {
    stage('Test coog image') {
      steps {
        parallel ( 
          "Paralell test 1": {
            container('coog') {
              script {
                sh '''
                  echo test 1
                  '''
              }
            }
          },
          "Paralell test 2": {
            container('coog') {
              script {
                sh '''
                    echo test 2
                  '''
              }
            }
          }
        )
      }
    }
    stage('Coucou') {
      steps {
        parallel ( 
          "Paralell test 1": {
            container('coog') {
              script {
                sh '''
                  echo test 1
                  '''
              }
            }
          },
          "Paralell test 2": {
            container('coog') {
              script {
                sh '''
                    echo test 2
                  '''
              }
            }
          }
        )
      }
    }
  }

  post {
    always {
      junit 'test-reports/TEST*.xml'
    }
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
