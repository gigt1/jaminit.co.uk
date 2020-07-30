pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        sh '''gem install bundler jekyll
bundle update
jekyll build
zip -r build _site'''
        archiveArtifacts(artifacts: 'build.zip', onlyIfSuccessful: true)
      }
    }

    stage('Deploy') {
      steps {
      if (env.BRANCH_NAME == 'master') {
            curl https://jaminit.co.uk/download.php
        }
        }
      }
    }

  }
}
