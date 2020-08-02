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
         stages {
            stage('gradle build') {
              echo 'executing gradle'
                withGradle() {
                sg './gradlew -v '
                }
        }
         }
        }
    }

