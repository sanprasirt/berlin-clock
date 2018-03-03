pipeline {
    agent any

    tools {
        jdk 'jdk8'
        maven 'maven3'
    }

    stages {
        stage('Install') {
            steps {
                sh "mvn -U clean test cobertura:cobertura -Dcobertura.report.format=xml"
            }
            post {
                always {
                    junit '**/target/*-reports/TEST-*.xml'
                    step([$class: 'CoberturaPublisher', coberturaReportFile: 'target/site/cobertura/coverage.xml'])
                }
            }
        }
        stage('Sonar') {
            steps {
                sh "mvn sonar:sonar -Dsonar.host.url=http://192.168.99.100:9000"
            }
        }
    }
}