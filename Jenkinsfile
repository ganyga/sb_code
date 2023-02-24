pipeline {
  agent any
  // any, none, label, node, docker, dockerfile, kubernetes
  tools{
    maven 'my_maven'
  }

  environmenet{
    gitName = 'gany'
    gitEmail = 'artzana03@gmail.com'
    gitWebaddress = 'https://github.com/ganyga/sb_code.git'
    gitSshaddress = 'git@github.com:ganyga/sb_code.git'
    gitCredential = 'git_cre' // github credential 생성시의 ID
  }

  stages {
    stage('Chekout Github') {
      steps {
        checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[credentialsId: gitCredential, url: gitWebaddress]]])
        }
      post {
        failuer {
            echo 'Repository clone failure'
        }
        success {
            echo 'Repository clone success'
        }
      }
    }

    stage('Maven Build') {
      steps {
        sh 'mvn clean install'
        // maven 플러그인이 미리 설치되어 있어야 함
        }
      post {
        failuer {
            echo 'maven build failure'
        }
        success {
            echo 'maven build success'
        }
      }
    }
  }
}
