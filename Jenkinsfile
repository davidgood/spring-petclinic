node {
  stage('SCM') {
    checkout scm
  }
  stage('SonarQube Analysis') {
    def mvn = tool 'Default Maven';
    sh "${mvn}/bin/mvn clean package"
  }
}
