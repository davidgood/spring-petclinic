pipeline {
  agent any
  stages {
    stage('SCM') {
      steps {
        checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/davidgood/spring-petclinic.git']]])      }
    }
    stage('gradle build') {
      steps {
        script {
          sh './gradlew build'
        }
      }
    }
    stage('deploy') {
      steps {
        ansiblePlaybook become: true, installation: 'Ansible', inventory: '/etc/ansible/hosts', playbook: 'playbook.yml'
      }
    }
  }
}
