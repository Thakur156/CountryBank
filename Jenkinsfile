pipeline {
    agent any

    stages {
        stage('git checkout') {
            steps {
                git 'https://github.com/Thakur156/CountryBank'
            }
        }
        stage('OWASP Dependency Check') {
            steps {
                 dependencyCheck additionalArguments: ' --scan ./ ', odcInstallation: 'DC'
                    dependencyCheckPublisher pattern: '**/dependency-check-report.xml'
            }
        }
        
        stage('Trivy') {
            steps {
                 sh "trivy fs ."
            }
        }
        
        stage('Build & deploy') {
            steps {
                sh "docker-compose up -d"
            }
        }
    }
}
