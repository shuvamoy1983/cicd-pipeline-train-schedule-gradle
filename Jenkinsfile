node {
   
   	stage 'Stage 1'
   		echo 'Hello there, shell scripts'
   	stage 'Checkout'
   		git credentialsId: 'github_api_key', url: 'https://github.com/shuvamoy1983/cicd-pipeline-train-schedule-gradle'
   	stage('zip git repo')
   	    dir('/var/lib/jenkins/workspace/') {
            sh '''
            zip -r  dist/algo.zip pipe
            '''
       }
   	stage('push To Stage')
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
                                        sourceFiles: '/dist/algo.zip',
                                        removePrefix: 'dist/',
                                        remoteDirectory: '/tmp',
                                        execCommand: 'unzip tmp/algo.zip -d /home/cloud_user/'
                                        
                                    )
                                ]
                            )
                        ]
                    )
                }
                
            
}
