pipeline {
    agent any

    parameters {
        choice choices: ['qa', 'prod', 'cloud'], description: 'Select environment for deployment', name: 'DEPLOY_TO'
    
        string(name: 'branch',
             defaultValue: '',
            description: 'Copy artifact from branch'
        )
    }

    stages {
        stage('Copy Artifact') {
            steps {
                copyArtifacts filter: 'sample', fingerprintArtifacts: true, 
                projectName: "sample-multibranch/${params.branch}", selector: upstream()
            }
        }
        stage('Deliver') {
            steps {
                withCredentials([sshUserPrivateKey(credentialsId: "vagrant-private-key", keyFileVariable: 'keyfile')]) {
                sh 'ANSIBLE_HOST_KEY_CHECKING=False ansible-playbook  --private-key=${keyfile} -i ${DEPLOY_TO}.ini  playbook.yml'
                }
            }
        } 
    }
}
