pipeline {
  agent any
  stages {
    stage('build') {
      steps {
        build 'TimeTrackerCopy'
      }
    }

    stage('Checkout') {
      steps {
        tool(name: 'Maven', type: 'Maven3.8.3')
        sh 'mvn complile'
      }
    }

    stage('Smoke tests') {
      steps {
        withMaven(maven: '3.8.3')
        sh 'mvn test'
      }
    }

    stage('Reports') {
      parallel {
        stage('Reports') {
          steps {
            junit '**/*.xml'
          }
        }

        stage('Regression Tests') {
          steps {
            withMaven(maven: '3.8.3')
            sh 'mvn test'
          }
        }

      }
    }

  }
}