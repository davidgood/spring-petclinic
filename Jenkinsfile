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
        script {
          def mvn = tool 'Default Maven';
          sh "${mvn}/bin/mvn package"
        }
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
