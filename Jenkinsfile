pipeline {
    agent { label 'master' }
    stages {
        stage('Deploy') {
            steps {
                sh 'ansible-playbook ./hello_world.yml -i /etc/ansible/inventory -u ubuntu' 
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
                    if (${RESPONSE} == 'HTTP/1.1 200 OK') {
                        echo ${RESPONSE}
                    } else {
                        echo 'Response code was not expected value'
                        exit 0
                    }  
                }
            }
        }
        stage('Cleanup') {
            steps {
                echo 'Nothing here yet'
            }
        }
    }
}