pipeline {
    agent {
        docker { 
            image 'salomaosan/ansible-alpine' 
            args '-u root:root'
        }
    }
    environment {
        VAUL_KEY=credentials('ansible_vault_key')
        GRAFANA=credentials('grafana_prod')
    }
    parameters {
        string (name: 'EMAIL', defaultValue: '', description: 'Informe o email do usuário.')
        choice (name: 'ROLE', choices: ['Viewer', 'Admin'], description: 'Informe o nome da Organização que será criada.')
        string (name: 'ORGANIZATION', defaultValue: '', description: 'Informe o nome da Organização que o usuário terá acesso.')
    }
    stages {
        stage('Create User') {
            steps{
                sh ('echo $VAUL_KEY > .vault_key')
                sh ('ansible-playbook -i hosts main.yml --tags "create-user-role" --vault-password-file .vault_key --extra-vars "user_email=\'${EMAIL}\'" --extra-vars "org_name=\'${ORGANIZATION}\'" --extra-vars="user_role=\'${ROLE}\'" --extra-vars=$GRAFANA_USR --extra-vars="grf_password=$GRAFANA_PSW"')
            }
        }
        stage('Extent User Flowti') {
            when { 
                environment name: 'ORGANIZATION', value: 'Flowti' 
            }
            steps{
                sh ('ansible-playbook -i hosts main.yml --tags "associate-user-to-orgs-role" --vault-password-file .vault_key --extra-vars "user_email=\'${EMAIL}\'" --extra-vars="user_role=\'${ROLE}\'" --extra-vars=$GRAFANA_USR --extra-vars="grf_password=$GRAFANA_PSW"')
            }
        }
    }
}
