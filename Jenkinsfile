def pageTitleTHIRDTestResult =''

pipeline {
    agent any

    stages {
        stage('Compile') {
            steps {
                echo 'First build'
                git branch: 'master', url: 'https://github.com/KasiaGrochal/TestJenkins.git'
                bat 'mvn clean compile'
                echo 'OK compile'
            }
        }
        stage('pageTitleTHIRDTest') {
            steps {
                bat 'mvn clean test -DEnv_Value='+environments+' -Dmaven.pageTitleTHIRD'
                echo 'OK test'
            }

            post {
                success {
                script{
                pageTitleTHIRDTestResult = 'success'
                }

                    }
                    failure{
                    script{
                    pageTitleTHIRDTestResult = 'failure'
                    }
                    }
                }
            }
            stage('pageTitleSECONDTest') {
                        steps {
                            bat 'mvn clean test -DEnv_Value='+environments+' -Dmaven.pageTitleSECOND'
                            echo 'OK test'
                        }

                        post {
                            always {
                                junit '**/target/surefire-reports/TEST-*.xml'
                                }
                            }
                        }
        }

        post{
        always{
        emailext to: 'testrest4747.2@gmail.com',
        mimeType: 'text/html',
        subject: 'Test',
        body: 'Test Results:'+
        'Result for pageTitleTHIRDTest: '+ pageTitleTHIRDTestResult

        }
        }
    }