pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                echo 'Running build automation'
                nodejs('Node-14.7') {
                sh 'yarn install'
                } 
            }
        }
         stage('gradle build') {
            steps {
              echo 'executing gradle'
                withGradle() {
                sh './gradlew -v'
                }
        }
         }
        }
    }

