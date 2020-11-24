pipeline {
    agent any
//    triggers { pollSCM('* * * * *') }
    stages {
        stage('Git copy') {
            steps {
                git 'https://github.com/PavelKozel/testautomation.git'
            }
        }
        stage('Syntax check') {
             steps {
                 powershell """cd Script_ebooks
                               pylint -f parseable project.py | tee pylint.out"""
            }
        }
        stage('Build') {
            steps {
                powershell """cd Script_ebooks
                              python project.py dev"""
            }
        }
//        stage('Test') {
//             steps {
//                 powershell """cd Test_framework
//                               python main.py dev"""
//            }
//        }
    }
    post {
        always {
            mail to: pavel_kozel@epam.com, subject: 'The Pipeline succeeded'
        }
        failure {
            mail to: pavel_kozel@epam.com, subject: 'The Pipeline failed'
        }
    }
}
