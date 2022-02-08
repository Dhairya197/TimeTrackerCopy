pipeline {
  agent any
  stages {
    stage('build') {
      steps {
        echo 'echo\'Build Started\' '
        sh 'npm install'
      }
    }

    stage('Checkout') {
      steps {
        git(url: 'https://github.com/Dhairya197/TimeTrackerCopy.git', branch: 'integration')
        withMaven(maven: 'Maven3.8.3') {
          sh 'mvn compile'
        }

      }
    }

    stage('Smoke tests') {
      steps {
        withMaven(maven: 'Maven3.8.3') {
          sh 'mvn test'
        }

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
            withMaven(maven: 'Maven3.8.3') {
              sh 'mvn test'
            }

          }
        }

      }
    }

  }
}