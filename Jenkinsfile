pipeline {
    agent any
    stages {
        stage('Git Checkout') {
            steps {
                git url: 'https://github.com/1stepaheaddv/calcwebapp'    
		            echo "Code Checked-out Successfully!!";
            }
        }
    stage('Package') {
       steps {
        sh 'mvn package' // Use 'sh' to execute shell commands
        echo "Maven Package Goal Executed Successfully!"
    }
  }
    stage('JUNit Reports') {
        steps {
            junit 'target/surefire-reports/*.xml'
		    echo "Publishing JUnit reports"
            }
        }
    stage('Jacoco Reports') {
        steps {
            jacoco()
            echo "Publishing Jacoco Code Coverage Reports";
            }
        } 

	stage('SonarQube analysis') {
            steps {
                withSonarQubeEnv('sonarqube-9.9') {
                sh 'mvn clean package sonar:sonar'
                }
            }
        }

	stage("Quality gate") {
            steps {
                waitForQualityGate abortPipeline: true
            }
        }
        
    }
    post {
        
        success {
            echo 'This will run only if successful'
        }
        failure {
            echo 'This will run only if failed'
        }
    
    }
}
