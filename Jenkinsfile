pipeline {
    agent {
        node{
            label 'maven'
        }
    }
enviroment {
    PATH = "/opt/apache-maven-3.9.7/bin:$PATH"
}

    stages {
        stage("build"){
            steps {
                sh 'mvn clean deploy'
            }
        }

    }
}
