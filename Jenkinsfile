node {
  stage('SCM') {
    checkout scm
  }
  stage('package') {
    def mvn = tool 'Default Maven';
    sh "${mvn}/bin/mvn clean package"
  }
}
