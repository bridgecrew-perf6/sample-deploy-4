pipeline {
    agent any

    stages {
        stage('Copy Artifact') {
            steps {
                copyArtifacts filter: 'sample', fingerprintArtifacts: true, projectName: 'sample', selector: lastSuccessful()
            }
        }
        stage('Deliver') {
            steps {
                sh 'scp ./sample vagrant@10.10.50.3'
            }
        }
       
    }
}   