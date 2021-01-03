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
        stage('Deploy to test env') {
            steps {
                configFileProvider([configFile(fileId: 'engineer365-kubeconfig', targetLocation: 'kubeconfig.yaml')]) {
                    sh 'kubectl --kubeconfig="./kubeconfig.yaml" apply -k overlays/test'
                }
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
