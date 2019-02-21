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
      steps {
        sh 'docker container run -d --name nodejs-app-sample -p 80:3000 nodejs-app-sample'
        sleep 10
        sh 'curl http://localhost:80'
      }
    }
    stage('Publish Image') {
      steps {
        sh 'docker image tag nodejs-app-sample:latest nodejs-app-sample:${env.BUILD_NUMBER}'
        withDockerRegistry([credentialsId: "c8e150dd-867b-4fd9-802e-b480d33f06d4", url: ""]) {
          sh 'docker image push garciacfer/nodejs-app-sample:${env.BUILD_NUMBER}'
          sh 'docker image push garciacfer/nodejs-app-sample:latest'
        }
      }
    }
  }
  post {
    always {
      sh 'docker container rm -f nodejs-app-sample'
    }
  }
}
