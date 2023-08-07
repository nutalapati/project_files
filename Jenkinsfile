pipeline {
    agent {
        node {
            label 'maven-agent'
        }
    }
environment {
       PATH = "/opt/apache-maven-3.9.3/bin:$PATH"
    }

    stages {
        stage('build') {
            steps {
                echo "------------- BUILD STARTED -------------"
                sh 'mvn clean deploy -Dmaven.test.skip=true'
                echo "------------- BUILD COMPLETED -------------"
            }
        }

        stage('Unit Test') {
            steps{
                echo "------------- UNIT TEST STARTED -------------"
                sh 'mvn surefire-report:report'
                echo "------------- UNIT TEST ENDED -------------"
            }
        }
        stage('SonarQube analysis') {
            environment {
              scannerHome = tool 'shiva-dp1'
            }
        steps {
            echo "------------- SONAR STARTED -------------"
         withSonarQubeEnv('shiva-dp1') { // If you have configured more than one global server connection, you can specify its name
         sh "${scannerHome}/bin/sonar-scanner"
         }

         echo "------------- SONAR ENDED -------------"

    }
    
  }
    }
}