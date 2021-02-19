var response = ""

pipeline {
    node("nodes") {
        stages {
            stage('Deploy') {
                steps {
                    sh 'ansible-playbook ./hello_world.yml -i /etc/ansible/inventory'
                }
            }
            stage('Test') {
                steps {
                    script {
                        response = sh (
                            script: 'curl http://172.31.89.200',
                            returnStdout: true
                            ).trim()
                    }
                }
            }
            stage('Verify') {

            echo "${response}"

            }
        }
    }  
}