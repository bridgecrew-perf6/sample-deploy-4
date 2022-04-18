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
                withCredentials([sshUserPrivateKey(credentialsId:'vagrant-private-key', keyFileVariable:'keyfile')])
                    sh 'scp -o "StrictHostKeyChecking=no" -i ${keyfile} ./sample vagrant@10.10.50.3:'
            }
        }
       
    }
}   