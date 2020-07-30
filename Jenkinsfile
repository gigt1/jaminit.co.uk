pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        sh 'cd /'
        sh 'ls | echo'
        
      }
    }

    stage('Test') {
      steps {
        sh 'cd /'
        sh 'ls | echo'
      }
    }

    stage('Deploy') {
      when {
        branch 'master'
      }
      steps {
        sh 'cd /'
        sh 'ls | echo'
      }
    }

  }
}
