pipeline {
    agent { label 'master' }
    stages {
        stage('Deploy') {
            steps {
                sh 'export ANSIBLE_HOST_KEY_CHECKING=False'
                sh 'ansible-playbook ./hello_world.yml -i /etc/ansible/inventory -u ubuntu --tags "create"' 
            }
        }
        stage('Test') {
            environment {
                RESPONSE = sh (
                        script: 'curl -Is http://${REMOTE_NODE} | head -n 1',
                        returnStdout: true
                        ).trim()
            }
            steps {
                script {
                    if (env.RESPONSE == 'HTTP/1.1 200 OK') {
                        echo "Reponse code was 200"
                    } else {
                        echo 'Response code was not expected value'
                        exit 0
                    }  
                }
            }
        }
        stage('Cleanup') {
            steps {
                sh 'ansible-playbook ./hello_world.yml -i /etc/ansible/inventory -u ubuntu --tags "remove"'
            }
        }
    }
}