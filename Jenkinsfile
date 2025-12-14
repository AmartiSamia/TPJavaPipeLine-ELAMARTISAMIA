pipeline {
  agent {
    docker {
      image 'my-maven-git:latest'
      args '-v $HOME/.m2:/root/.m2'
    }
  }

  stages {
    stage('Checkout') {
      steps {
        checkout scm
      }
    }

    stage('Build & Test') {
      steps {
        dir('Java_project') {
          sh 'mvn clean test package'
        }
      }
    }

    stage('Run Jar') {
      steps {
        dir('Java_project') {
          sh 'java -jar target/*.jar'
        }
      }
    }
  }
}
