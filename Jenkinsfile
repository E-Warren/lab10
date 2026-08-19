pipeline {
    agent any
    tools {
        maven 'Maven3' // Specify the Maven installation name configured in Jenkins}
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
        stage('Code Coverage') {
            steps {
                sh 'mvn -B jacoco:report'
            }
        }
        stage('Archive') {
            steps {
                archiveArtifacts artifacts: 'target/*.jar,target/site/jacoco**', fingerprint: true
            }
        }
    }
}
