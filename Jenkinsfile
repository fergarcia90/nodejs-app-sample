pipeline {
  agent any

  stages {
    stage('Build') {
      steps {
        checkout scm
        sh 'docker image build -t nodejs-app-sample .'
      }
    }
    stage('Test image') {
      sh 'docker container run -d --name nodejs-app-sample -p 80:3000 nodejs-app-sample'
      sh 'curl http://localhost:80'
      sh 'docker container rm -f nodejs-app-sample'
    }
  }
}
