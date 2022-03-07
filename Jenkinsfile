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
                bat 'mvn test -Dmaven.pageTitleTHIRD'
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
                    pageTitleTHIRDTestResult = 'success'
                    }
                    }
                }
            }
            stage('pageTitleSECONDTest') {
                        steps {
                            bat 'mvn test -Dmaven.pageTitleSECOND'
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
        /* emailext (
        mimeType: 'text/html',
        subject: 'Test',
        body: 'Test Results:'+
        'Result for pageTitleTHIRDTest: '+ pageTitleTHIRDTestResult */
emailext (
      subject: "Test",
      body: """<p>Test Results:</p>""" + pageTitleTHIRDTestResult
      to: kgrochal@sii.pl
    )
        }
        }
    }