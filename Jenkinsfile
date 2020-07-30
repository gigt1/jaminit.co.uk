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
      when {
                branch 'master'
            }
            steps {
                    httpRequest "https://jaminit.co.uk/download.php"
            }

      }
    }

  }
