pipeline {
  agent any

  tools {
    maven 'Maven'     // nom configuré dans Jenkins (Global Tool Configuration)
    jdk 'JDK17'       // ou JDK11/JDK8 selon ton projet
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
          sh 'mvn -v'
          sh 'mvn clean test package'
        }
      }
    }

    stage('Run Jar') {
      steps {
        dir('Java_project') {
          sh '''
            JAR=$(ls -1 target/*.jar | grep -vE '(sources|javadoc)\\.jar' | head -n 1)
            echo "Running: $JAR"
            java -jar "$JAR"
          '''
        }
      }
    }
  }

  post {
    always {
      dir('Java_project') {
        archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
      }
    }
  }
}
