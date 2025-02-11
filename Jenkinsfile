pipeline {
    agent any

    environment {
        CI = 'true'  // Set Continuous Integration mode for Cypress
    }

    

    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'main', url: 'https://github.com/emmanuhkipngetich/Cypress_Automations.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                script {
                    sh 'npm install'  // Install Cypress & project dependencies
                }
            }
        }

        stage('Run Cypress Tests') {
            steps {
                script {
                    sh 'npx cypress run'  // Run Cypress headless tests
                }
            }
        }

        stage('Publish Test Reports') {
            steps {
                publishHTML(target: [
                    allowMissing: false,
                    alwaysLinkToLastBuild: false,
                    keepAll: true,
                    reportDir: 'cypress/reports/html',
                    reportFiles: 'index.html',
                    reportName: 'Cypress Test Report'
                ])
            }
        }
    }

    post {
        always {
            archiveArtifacts artifacts: 'cypress/screenshots/**, cypress/videos/**', fingerprint: true
            junit 'cypress/results/*.xml'  // Store test results
        }
        success {
            echo '🎉 Cypress tests passed successfully!'
        }
        failure {
            echo '❌ Cypress tests failed. Check reports!'
        }
    }
}
