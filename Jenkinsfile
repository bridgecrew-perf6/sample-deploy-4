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
                withCredentials([sshUserPrivateKey(credentialsId: "vagrant-private-key", keyFileVariable: 'keyfile')]) {
                sh 'ANSIBLE_HOST_KEY_CHECKING=False ansible-playbook  --private-key=${keyfile} -i hosts.ini playbook.yml'
                }
            }
        } 
    }
}
