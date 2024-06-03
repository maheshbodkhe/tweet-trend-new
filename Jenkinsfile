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
                echo "---------------Build test started------------"
                sh 'mvn clean deploy -Dmaven.test.skip=true'
                echo "---------------Build test completed------------"
            }
        }
        stage("test"){
            steps{
                echo "---------------unit test started------------"
                sh 'mvn surefile-report:report'
                echo "---------------unit test completed------------"
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
  stage("Quality Gate"){
    steps{
        script{
    timeout(time:1, unit: 'HOURS')
    def qg = waitForQualityGate()
    if (qg.staus != 'OK')
      error "Pipeline aborted due to quality gate failure: $(qg.status)"
    }
  }
}
   }
 }
}
}