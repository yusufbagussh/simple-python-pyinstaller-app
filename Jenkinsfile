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
    stage('Manual Approve') {
        input message: 'Sudah selesai menggunakan React App? (Klik "Proceed" untuk mengakhiri)' 
    }
    stage('Deploy') {
        sh 'sleep 60'
    }
}

// pipeline {
//     agent none
//     stages {
//         stage('Build') {
//             agent {
//                 docker {
//                     image 'python:2-alpine'
//                 }
//             }
//             steps {
//                 sh 'python -m py_compile sources/add2vals.py sources/calc.py'
//             }
//         }
//         stage('Test') {
//             agent {
//                 docker {
//                     image 'qnib/pytest'
//                 }
//             }
//             steps {
//                 sh 'py.test --verbose --junit-xml test-reports/results.xml sources/test_calc.py'
//             }
//         }
//         stage('Deliver') {
//             agent {
//                 docker {
//                     image 'cdrx/pyinstaller-linux:python2'
//                 }
//             }
//             steps {
//                 sh 'sleep 60'
//                 sh 'pyinstaller --onefile sources/add2vals.py'
//             }
//             post {
//                 success {
//                     archiveArtifacts 'dist/add2vals'
//                 }
//             }
//         }
//     }
// }
