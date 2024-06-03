pipeline {
    agent {
        node{
            label 'maven'
        }
    }
environment {
    PATH = "/opt/apache-maven-3.9.7/bin:$PATH"
}

    stages {
        stage("build"){
            steps {
                sh 'mvn clean deploy'
            }
        }
        stage('SonarQube analysis') {
        environment {
          scannerHome = tool 'mahesh-sonar-scanner'
        }
        steps {
        withSonarQubeEnv('mahesh-sonarqube-server'){
           sh "${scannerHome}/bin/sonar-scanner"
        }
        }
      }
    }
    }
