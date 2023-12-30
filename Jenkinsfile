node {
    stage('Build') {
        docker.image('python:2-alpine').inside {
            sh 'python -m py_compile sources/add2vals.py sources/calc.py'
        }
    }
    stage('Test') {
        docker.image('qnib/pytest').inside {
            sh 'py.test --verbose --junit-xml test-reports/results.xml sources/test_calc.py'
        }
    }
    stage('Deploy') {
        docker.image('python:3-alpine').inside('-u root')  {
            sh 'apk add --no-cache py3-pip binutils'
            sh 'pip3 install pyinstaller'
            sh 'pyinstaller --onefile sources/add2vals.py'
            sh 'sleep 60s'
        }
    }
}