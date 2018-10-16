pipeline {
  agent {
    kubernetes {
      label 'maven-3.5.4-pod-template'
      defaultContainer 'maven-3.5.4-container'
      yamlFile 'KubernetesPod.yaml'
    }
  }
  stages {
    stage('Build') {
      steps {
        container('maven-3.5.4-container') {
          sh 'mvn -B -DskipTests clean package'
        }
      }
    }
    stage('Test') {
      steps {
        sh 'mvn test'
      }
      post {
        always { 
          junit '**/*.xml'
        }
      }
    }
    stage('Deliver') {
      steps {
        sh 'jenkins/scripts/deliver.sh'
      }
    }
  }
}
