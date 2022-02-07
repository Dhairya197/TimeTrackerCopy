pipeline {
  agent any
  stages {
    stage('build') {
      steps {
        withMaven(maven: '3.8.3')
        git(url: 'https://github.com/Dhairya197/TimeTrackerCopy.git', branch: 'integration')
      }
    }

    stage('Checkout') {
      steps {
        sh 'mvn compile'
        withMaven(maven: '3.8.3')
      }
    }

    stage('Smoke tests') {
      steps {
        sh 'mvn test'
        withMaven(maven: '3.8.3')
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
            sh 'mvn test'
            withMaven(maven: '3.8.3')
          }
        }

      }
    }

  }
}