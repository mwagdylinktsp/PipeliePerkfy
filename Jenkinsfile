pipeline {
  agent any
  stages {
    stage('SCM') {
      steps {
        git(url: 'git@github.com:360CXservices/Perkfy-Service.git', branch: 'main', credentialsId: 'Jenkins-LiveOpen', poll: true)
        echo 'SCM Poll Done'
        powershell 'Remove-Item C:\\JenkinsData\\jenkins_home\\workspace\\PipeliePerkfy_main\\Perkfy.Web\\bin\\Release\\net8.0* -recurse -force'
      }
    }

    stage('Build') {
      steps {
        bat 'dotnet build C:\\JenkinsData\\jenkins_home\\workspace\\PipeliePerkfy_main\\Perkfy.sln'
        echo 'Build Done'
      }
    }

    stage('Configuration to Release') {
      steps {
        bat 'iisreset /stop'
        powershell 'Remove-Item d:\\iis\\perkfy\\* -recurse -force'
      }
    }

    stage('Move and Run The New Build') {
      steps {
        powershell 'Copy-Item -Path D:\\GitHub_Projects\\Perkfy\\Perkfy.Web\\bin\\Debug\\net8.0\\* -Destination D:\\iis\\Perkfy -Recurse -force'
        bat 'iisreset /start'
      }
    }

    stage('Done Massage') {
      steps {
        echo 'Project is running now '
      }
    }

  }
  environment {
    dotnet = 'C:\\Program Files\\dotnet\\dotnet.exe'
  }
}