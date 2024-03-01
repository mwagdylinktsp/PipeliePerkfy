pipeline {
  agent any
  stages {
    stage('SCM') {
      steps {
        git(url: 'git@github.com:mwagdylinktsp/perkfy.git', branch: 'main', credentialsId: 'Word-SSH')
        echo 'SCM Poll Done'
        bat 'del /s /q D:\\GitHub_Projects\\Perkfy\\Perkfy.Web\\bin\\Debug\\net8.0\\'
      }
    }

    stage('Build') {
      steps {
        bat 'dotnet build D:\\GitHub_Projects\\Perkfy\\Perkfy.Web\\Perkfy.Web.csproj'
        echo 'Build Done'
      }
    }

    stage('Configuration to Release') {
      steps {
        bat 'iisreset /stop'
        bat 'del /s /q "D:\\New folder\\Perkfy"'
      }
    }

    stage('Move and Run The New Build') {
      steps {
        bat 'robocopy "D:\\GitHub_Projects\\Perkfy\\Perkfy.Web\\bin\\Debug\\net8.0" "D:\\New folder\\Perkfy" /mir'
        bat 'iisreset /start'
      }
    }

    stage('Done Massage') {
      steps {
        echo 'Project is running now '
      }
    }

  }
}