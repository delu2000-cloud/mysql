def app
pipeline {
  agent {
    dockerfile true 
  }

  stages {
    stage('Clone repository') {
      checkout scm
    }
    stage('Build image') {
      app = docker.image('mysql:5').withRun('-e "MYSQL_ROOT_PASSWORD=my-secret-pw" -p 3306:3306') {
        sh 'while ! mysqladmin ping -h0.0.0.0 --silent; do sleep 1; done'
        sh 'make check'
      }
    }
  }
}
