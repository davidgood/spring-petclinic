pipeline {
  agent any
  options {
    skipDefaultCheckout(true)
  }
  stage('SCM') {
    checkout scm
  }
  stage('package') {
    def mvn = tool 'Default Maven';
    sh "${mvn}/bin/mvn clean package"
  }
  stage('deploy') {
    ansiblePlaybook become: true, installation: 'Ansible', inventory: '/etc/ansible/hosts', playbook: 'playbook.yml'
  }
  post {
    always {
      cleanWs notFailBuild: true
    }
  }
}
