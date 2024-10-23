pipeline {
    agent any 
    stages {
        stage('Build') { 
            steps {
                sh 'python3 -m py_compile sources/add2vals.py sources/calc.py' 
                stash(name: 'compiled-results', includes: 'sources/*.py*') 
            }
        }
        stage('Install Pytest') {
            steps {
                // Installing pytest using pip
                sh 'pip install pytest'
            }
        }
        stage('Test') {
            steps {
                // Running the tests using pytest
                sh 'pytest --junit-xml test-reports/results.xml sources/test_calc.py'
            }
            post {
                always {
                    junit 'test-reports/results.xml'
                }
            }
        }
    }
}
