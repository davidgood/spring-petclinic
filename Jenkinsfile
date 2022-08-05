pipeline {
  agent any
  stages {
    stage('SCM') {
      steps {
        checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/davidgood/spring-petclinic.git']]])      }
    }
    stage('package') {
      steps {
        script {
          sh './gradlew build -x check'
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

