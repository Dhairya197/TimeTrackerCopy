pipeline {
  agent any
  stages {
    stage('build') {
      steps {
        sh 'mvn build'
        withMaven(maven: '3.8.3')
      }
    }

    stage('Checkout') {
      steps {
        git(url: 'https://github.com/Dhairya197/TimeTrackerCopy.git', branch: 'integration')
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
            withMaven(maven: '3.8.3')
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