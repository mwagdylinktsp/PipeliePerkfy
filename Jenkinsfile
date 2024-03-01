pipeline {
  agent any
  stages {
    stage('SCM') {
      steps {
        git(url: 'git@github.com:mwagdylinktsp/perkfy.git', branch: 'main', credentialsId: 'Word-SSH')
        echo 'SCM Poll Done'
      }
    }

    stage('Build') {
      steps {
        bat 'dotnet build D:\\GitHub_Projects\\Perkfy\\Perkfy.Web\\Perkfy.Web.csproj'
        echo 'Build Done'
      }
    }

  }
}