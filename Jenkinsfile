pipeline {
    agent {
        kubernetes {
            cloud 'rsys-devel'
            defaultContainer 'miniforge3'
            inheritFrom 'miniforge'
        }
    }
    
    stages {
        stage ("install") {
            steps {
                sh 'conda install python==3.12.7 pip -y -q'
                sh 'useradd galaxy -m'
                sh 'apt-get update'
                sh 'apt-get install sudo -y'
                sh 'pip install -r requirements.txt'
            }
        }
        stage ("lint") {
            steps {
                sh "sudo -u galaxy planemo lint autobigs-cli.xml"
            }
        }
        stage ("test") {
            steps {
                sh 'sudo -u galaxy mkdir test_results'
                sh "sudo -u galaxy planemo test autobigs-cli.xml --test_output_junit test_results/junit_results.xml --test_output_json test_results/results.json --test_output test_results/human.html"
                xunit checksName: '', tools: [JUnit(excludesPattern: '', pattern: 'test_results/junit_report.xml', stopProcessingIfError: true)]
            }
        }
    }
}