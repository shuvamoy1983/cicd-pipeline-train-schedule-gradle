pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                echo 'Running build automation'
                sh './gradlew build --no-daemon'
                archiveArtifacts artifacts: '/var/lib/jenkins/workspace/train/dist/trainSchedule.zip'
            }
        }
        
        stage('push To Stage') {
            when {
                branch 'master'
            }
            steps {
                withCredentials([usernamePassword(credentialsId: 'webserver_login', passwordVariable: 'USERPASS', usernameVariable: 'USERNAME')]) {
                sshPublisher(
                        failOnError: true,
                        continueOnError: false,
                        publishers: [
                            sshPublisherDesc(
                                configName: 'staging',
                                sshCredentials: [
                                    username: "$USERNAME",
                                    encryptedPassphrase: "$USERPASS"
                                ], 
                                transfers: [
                                    sshTransfer(
                                        sourceFiles: '/var/lib/jenkins/workspace/train/dist/trainSchedule.zip',
                                        removePrefix: 'var/lib/jenkins/workspace/train/dist/',
                                        remoteDirectory: '/tmp',
                                        execCommand: 'sudo unzip /tmp/trainSchdule.zip -d /opt/train-schedule &&  sudo /usr/bin/systemctl start train-schedule'
                                        
                                    )
                                ]
                            )
                        ]
                    )
                }
                }
            }
        }
    }

