pipeline {
    agent {
        kubernetes {
            cloud 'rsys-devel'
            defaultContainer 'pip'
            inheritFrom 'pip'
        }
    }
    
    stages {
        stage ("install") {
            steps {
                sh 'useradd galaxy -m'
                sh 'apt update'
                sh 'apt install sudo -y'
                sh 'pip install -r requirements.txt'
                sh 'pip install standard-imghdr'
            }
        }
        stage ("lint") {
            steps {
                sh "planemo lint autobigs-cli.xml"
            }
        }
        stage ("test") {
            steps {
                sh 'mkdir test_results'
                sh "sudo -u galaxy planemo test autobigs-cli.xml --test_output_junit test_results/junit_results.xml --test_output_json test_results/results.json --test_output test_results/human.html"
                xunit checksName: '', tools: [JUnit(excludesPattern: '', pattern: 'test_results/junit_report.xml', stopProcessingIfError: true)]
            }
        }
    }
}