pipeline {
    agent {
        node {
            label "workstation"
        }
    }

    options {
        ansiColor('xterm')
    }

    parameters {
        choice(name: 'ACTION', choices: ['apply', 'destroy'], description: 'Choose TF Action')
    }

    stages {
        stage('DEV') {
            steps {
                sh 'terraform init -reconfigure -backend-config=dev-env/state.tfvars'
                sh 'terraform init -backend-config=dev-env/state.tfvars'
                sh 'terraform ${ACTION} -auto-approve -var-file=dev-env/main.tfvars'
            }
        }

        stage('PROD') {
            steps {
                sh 'terraform init -reconfigure -backend-config=prod-env/state.tfvars'
                sh 'terraform init -backend-config=prod-env/state.tfvars'
                sh 'terraform ${ACTION} -auto-approve -var-file=prod-env/main.tfvars'
            }
        }
    }

    post {
        always {
            cleanWs()
        }
    }
}
