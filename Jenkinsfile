pipeline {
  agent any
  // any, none, label, node, docker, dockerfile, kubernetes
  tools{
    maven 'my_maven'
  }

  environment{
    gitName = 'gany'
    gitEmail = 'artzana03@gmail.com'
    gitWebaddress = 'https://github.com/ganyga/sb_code.git'
    gitSshaddress = 'git@github.com:ganyga/sb_code.git'
    gitCredential = 'git_cre' // github credential 생성시의 ID
    dockerHubRegistry = 'gaeunoo/sbimage'
  }

  stages {
    stage('Chekout Github') {
      steps {
        checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[credentialsId: gitCredential, url: gitWebaddress]]])
        }
      post {
        failure {
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
        failure {
            echo 'maven build failure'
        }
        success {
            echo 'maven build success'
        }
      }
    }
    
    stage('Docker image Build') {
      steps {
        sh "docker build -t ${dockerHubRegistry}:${currentBuild.number} ."
        sh "docker build -t ${dockerHubRegistry}:latest ."       
        // currentBuild.number 젠킨스에서 제공하는 빌드넘버 변수
        }
      post {
        failure {
            echo 'docker image build failure'
        }
        success {
            echo 'docker image build success'
        }
      }
    }
  }
}
