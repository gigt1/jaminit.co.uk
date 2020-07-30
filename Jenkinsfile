pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        sh '''gem install bundler jekyll
bundle update
jekyll build
zip -r build _site'''
      }
    }

  }
}