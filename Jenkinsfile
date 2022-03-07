def test1Result =''

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
                always {
                    junit '**/target/surefire-reports/TEST-*.xml'
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
    }