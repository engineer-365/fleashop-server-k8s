// See
//  - https://www.jenkins.io/doc/book/pipeline/
//  - https://builder.engineer365.org:40443/pipeline-syntax/

pipeline {
    agent any
    options {
        skipStagesAfterUnstable()
        timestamps()
    }
    stages {
        stage('Deploy') {
            withCredentials([string(credentialsId: 'cloud_user_pw', variable: 'USERPASS')]) {
                sshPublisher(
                    failOnError: true,
                    publishers: [
                        sshPublisherDesc(
                            configName: 'staging',
                            sshCredentials: [
                                username: 'cloud_user',
                                encryptedPassphrase: "$USERPASS"
                            ], 
                            transfers: [
                                sshTransfer(
                                    sourceFiles: 'src/**',
                                    removePrefix: 'src/'
                                )
                            ]
                        )
                    ]
                )
            }
        }
    }
    post {
        always {
            // "chucknorris" plugin
            chuckNorris()

            // "git-forensics" plugin
            // TODO: not yet enabled, actually
            mineRepository()
        }
    }
}
