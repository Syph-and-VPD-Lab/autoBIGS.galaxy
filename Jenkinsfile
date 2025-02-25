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
                sh 'pip install -r requirements.txt'
                sh 'pip install standard-imghdr'
                sh 'planemo ci_setup'
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
                sh "planemo test autobigs-cli.xml --test_output_junit test_results/junit_results.xml --test_output_json test_results/results.json --test_output test_results/human.html"
                xunit checksName: '', tools: [JUnit(excludesPattern: '', pattern: 'test_results/junit_report.xml', stopProcessingIfError: true)]
            }
        }
    }
}