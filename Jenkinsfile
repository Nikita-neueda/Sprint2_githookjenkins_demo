pipeline {
    agent any
     tools {
        // This injects the Java 21 paths you configured in Step 1
        jdk 'JDK21'
        maven 'Maven3'
    }
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        stage('Build') {
            steps {
                sh 'mvn -B clean package'
                echo 'Build completed successfully!'
		
            }
        }
        stage('Test') {
            steps {
                
                sh 'mvn -B test'
                
            }
            post {
                always {
                    junit 'target/surefire-reports/*.xml'
                }
            }
        }
        stage('Archive') {
            steps {
                archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
            }
        }
    }
}
