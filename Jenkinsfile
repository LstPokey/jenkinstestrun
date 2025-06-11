pipeline {
  agent any

  stages {
    stage('Build & Test in Docker') {
      steps { 
        script {
          def img = docker.image('python3.9')
          img.pull()
          img.inside('-u root:root') {
            checkout scm
            sh 'pip install pyflakes pytest'
            sh 'pytest *.py'
            sh 'pytest --maxfail=1 --disable-waringngs -q'
          }
        }
      }
    }
  }

  post {
    success {
      echo 'Build und Test erflogreich'
    }
    failure {
      echo 'Build fehlgeschlagen ist'
    }
  }
}
