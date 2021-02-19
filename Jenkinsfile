pipeline {
    agent nodes
    stages {
        stage('Deploy') {
            steps {
                sh 'ansible-playbook ./hello_world.yml -i /etc/ansible/inventory'
            }
        }
        stage('Test') {
            steps {
                RESPONSE = sh (
                    script: 'curl http://172.31.89.200',
                    returnStdout: true
                    ).trim()
                echo "${RESPONSE}"
            }
        }
    }
}