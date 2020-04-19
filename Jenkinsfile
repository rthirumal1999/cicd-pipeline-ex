pipeline {
    agent any
    stages {
        stage('SCM') {
            steps {
                scm checkout
            }
        }
        stage('Compile'){
            steps {
                sh "./gradlew compileJava"
            }
        }
        stage('Junit'){
            steps {
                sh "./gradlew test"
            }
        }
        stage('Sonar'){
            environment {
                stagecannerHome = tool 'SonarQubeScanner'
            }
            steps {
                withSonarQubeEnv('sonarqube') {
                    sh "${scannerHome}/bin/sonar-scanner"
                }
                timeout(time: 10, unit: 'MINUTES') {
                    waitForQualityGate abortPipeline: true
                }
            }
        }
    }
}