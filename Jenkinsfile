pipeline {
    agent any

    tools {
        maven "maven"
    }

    stages {
        stage ("Git clone") {
            steps {
                git branch: 'main', url: 'https://github.com/Candy-DevOps/web-app.git'
            }
        }
        stage ("Build and Package with Maven") {
            steps {
                sh '''
                mvn clean
                mvn package
                '''
            }
        }
        stage (Sonaqube Analysis) {
            environment {
                ScannerHome = tool 'Sonar'
            }
            steps {
                script {
                    withSonarQubeEnv(credentialsId: 'sonarqube-ID') {
                        sh "${ScannerHome}/bin/sonar-scanner -Dsonar.projectKey=Jomacs"
                    }
                }
            }
        }
        
    }
}
