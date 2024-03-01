pipeline {
  agent any
  stages {
    stage('SCM') {
      parallel {
        stage('SCM') {
          steps {
            git(url: 'git@github.com:mwagdylinktsp/perkfy.git', branch: 'main', credentialsId: 'Word-SSH')
            echo 'SCM Poll Done'
          }
        }

        stage('Del Old Build') {
          steps {
            bat 'del /s /q D:\\GitHub_Projects\\Perkfy\\Perkfy.Web\\bin\\Debug\\net8.0\\'
          }
        }

      }
    }

    stage('Build') {
      steps {
        bat 'dotnet build D:\\GitHub_Projects\\Perkfy\\Perkfy.Web\\Perkfy.Web.csproj'
        echo 'Build Done'
      }
    }

    stage('Configuration to Release') {
      parallel {
        stage('Stop IIS') {
          steps {
            bat 'iisreset /stop'
          }
        }

        stage('Del Old Data') {
          steps {
            bat 'del /s /q D:\\New folder\\Perkfy\\'
          }
        }

      }
    }

    stage('Deploy') {
      parallel {
        stage('Move The New Build to IIS') {
          steps {
            bat 'robocopy "D:\\GitHub_Projects\\Perkfy\\Perkfy.Web\\bin\\Debug\\net8.0" "D:\\New folder\\Perkfy" /mir'
          }
        }

        stage('Run IIS') {
          steps {
            bat 'iisreset /start'
          }
        }

      }
    }

    stage('Done Massage') {
      steps {
        echo 'Project is running now '
      }
    }

  }
}