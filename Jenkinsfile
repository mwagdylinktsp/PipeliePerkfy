pipeline {
  agent any
  stages {
    stage('SCM') {
      steps {
        git(url: 'git@github.com:mwagdylinktsp/perkfy.git', branch: 'main', credentialsId: 'Word-SSH', poll: true)
      }
    }

  }
}