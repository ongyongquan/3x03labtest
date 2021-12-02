pipeline {
        agent any
        stages {
                stage('OWASP DependencyCheck') {
                    steps {
                        dependencyCheck additionalArguments: '--format HTML --format XML', odcInstallation: 'OWASP'
                    }
                }
                stage('Unit Test') {
                    steps {
                        echo 'Testing...'
                        sh 'python3 -m pip install -r web/unitrequirements.txt'
                        sh 'python3 web/secretlap/test/customerUnitTest.py'     
                    }
                }
        }
        post {
                success {
                    dependencyCheckPublisher pattern: 'dependency-check-report.xml'
                }
                always {
                    junit testResults: 'test-reports/*.xml'
                }
        }
}