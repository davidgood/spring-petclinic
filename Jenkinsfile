pipeline {
  agent any
  stages {
    stage('SCM') {
      steps {
        checkout scm
      }
    }
    stage('package') {
      steps {
        def mvn = tool 'Default Maven';
        sh "${mvn}/bin/mvn clean package"
      }
    }
    stage('deploy') {
      steps {
        ansiblePlaybook become: true, installation: 'Ansible', inventory: '/etc/ansible/hosts', playbook: 'playbook.yml'
      }
    }
  }
  post {
    always {
      cleanWs notFailBuild: true
    }
  }
}
