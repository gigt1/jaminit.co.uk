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
        sh 'bundle exec htmlproofer ./_site --check-html --disable-external --allow_hash_href'
      }
    }

    stage('Deploy') {
      when {
        branch 'master'
      }
      steps {
        sh 'wget "https://jaminit.co.uk/download.php"'
      }
    }

  }
}