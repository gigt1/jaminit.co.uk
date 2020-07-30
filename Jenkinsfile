pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        sh '''gem install bundler jekyll
bundle update
jekyll build
zip -r build _site'''
        archiveArtifacts(artifacts: 'build.zip', onlyIfSuccessful: true, fingerprint: true)
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
