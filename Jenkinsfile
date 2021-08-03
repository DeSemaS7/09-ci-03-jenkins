pipeline {
    agent any
    stages {
        stage("Git checkout"){
            steps {
                git credentialsId: '686047b4-03ee-4162-93d3-069ff9913c39', url: 'git@github.com:DeSemaS7/example-playbook.git'
            }
        }
        stage("show dir"){
            steps {
                sh 'ls -la'
                }
        }
        stage("download prereqs"){
            steps {
            sh 'ansible-vault decrypt secret --vault-password-file vault_pass'
            sh 'mv ./secret ~/.ssh/id_rsa'
            sh 'chmod 400 ~/.ssh/id_rsa'
            sh 'ansible-galaxy install -r requirements.yml -p roles'
            }
        }
        stage("Run playbook"){
            steps {
                ansiblePlaybook(
                    playbook: 'site.yml',
                    inventory: 'inventory/prod.yml',
                    )
            }
        }
    }
}
