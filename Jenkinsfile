pipeline { 
    agent any 
    stages { 
        stage('Cloning our Git') { 
            steps { 
                git branch:'main', url: 'https://github.com/athiboo/ans_test.git' 
            }
        }

        stage('Provision the Terraform Infra') {
            steps {
                echo 'Init the Terraform to Download and Apply Terraform with -auto-approve option'
                sh '''
                cd terraforminfra
                terraform init
                terraform validate
                terraform fmt
                echo "its time to apply the code"
                terraform apply -auto-approve
                '''
            }
        }
        stage('ansible') {
            steps {
                echo 'here'
                sh '''
                ansible-playbook aplaybooksapp2/playbook.yml -i aplaybooksapp2/inventory
                '''
            }
        }
        stage('Dummy2') {
            steps {
                echo 'Hello World'
            }
        }
    }
    post{
        always{
            archiveArtifacts artifacts: 'bandit-output.json',onlyIfSuccessful: true
        }
    }
}