pipeline {
  agent any

  triggers {
    pollSCM('* * * * *')
  }

  stages {
    stage('Checkout') {
      steps {
        git branch: 'main', 
        url: 'https://github.com/lizen5/cicd-test.git'
      }
    }
    stage('Build') {
      steps {
        sh 'mvn clean package -DskipTest=true'
      }
    }
    stage('Test') {
      steps {
        sh 'mvn test'
      }
    }
    stage('Deploy') {
      steps {
        deploy adapters: [tomcat9(credentialsId: 'tomcat-manager', url: '192.168.56.102:8080')], contextPath: null, war: 'target/hello-world.war'
      }
    }
  }
}
