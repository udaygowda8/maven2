pipeline {
  agent {
    kubernetes {
      label 'pod-template-maven-3.5.4'
      defaultContainer 'jnlp'
      yamlFile 'KubernetesPod.yaml'
    }
  }
  stages {
    stage('Build') {
      steps {
        container('maven-container') {
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
