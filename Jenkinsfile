pipeline {
    agent any

    tools {
        // Use the Maven installation configured in Jenkins (ensure the name matches)
        maven "maven3"
    }

    stages {
        stage('Checkout Code') {
            steps {
                // Clone the repository from GitHub
                git 'https://github.com/ioannis-mac/projet-maven.git'
            }
        }
        stage('Build Maven') {
            steps {
                // Run Maven build and package the application
                sh "mvn -Dmaven.test.failure.ignore=true clean package"
            }
            post {
                // Post-build actions
                success {
                    // Record test results
                    junit '**/target/surefire-reports/TEST-*.xml'
                    // Archive the built jar file
                    archiveArtifacts 'target/*.jar'
                }
                failure {
                    // Optionally handle the failure case
                    echo 'Build failed!'
                }
            }
        }
    }
}
