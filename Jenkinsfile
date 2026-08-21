pipeline {
    agent any
     tools {
        // This injects the Java 21 paths you configured in Step 1
        jdk 'JDK21'
    }
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        stage('Build') {
            steps {
		 
                sh 'mvn -f ./starter/pom.xml -B clean package'
		
            }
        }
        stage('Test') {
            steps {
                
                sh 'mvn -f ./starter/pom.xml -B test'
                
            }
            post {
                always {
                    junit 'starter/target/surefire-reports/*.xml'
                }
            }
        }
        stage('Archive') {
            steps {
                archiveArtifacts artifacts: 'starter/target/*.jar', fingerprint: true
            }
        }
    }
}
