pipeline {
  agent any
  stages {
    stage('build') {
      steps {
        withMaven(maven: '3.8.3')
        build(job: 'TimeTrackerCopy', wait: true, quietPeriod: 10)
      }
    }

    stage('Checkout') {
      steps {
        withMaven(maven: '3.8.3')
        git(url: 'https://github.com/Dhairya197/TimeTrackerCopy.git', branch: 'integration')
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