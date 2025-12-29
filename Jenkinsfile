pipeline {
    agent any

    stages {

        stage('Build') {
            steps {
                echo "Building the war"
            }
        }

        stage('Deploy to QA') {
            steps {
                echo "Deploying to QA"
            }
        }

        stage('Pull Docker Images') {
            parallel {

                stage('Pull GoRest Image') {
                    steps {
                        bat 'docker pull vijayalakshminirmal/datadrivenapitest2:1.0'
                    }
                }

                stage('Pull Booking Image') {
                    steps {
                        bat 'docker pull vijayalakshminirmal/gorestapitest:1.0'
                    }
                }
            }
        }

        stage('Prepare Newman Results Directory') {
            steps {
                bat 'mkdir -p %cd%\\newman'
            }
        }

        stage('Run API Test Cases in Parallel') {
            parallel {

                stage('Run Data driven Tests') {
                    steps {
                        bat 'docker run --rm -v %cd%\\newman:/app/results vijayalakshminirmal/datadrivenapitest2:1.0'
                    }
                }

                stage('Run GoRest API Tests') {
                    steps {
                        bat 'docker run --rm -v %cd%\\newman:/app/newman vijayalakshminirmal/gorestapitest:1.0'
                    }
                }
            }
        }
        stage('Publish HTML Extra Reports') {
            parallel {
                stage('Publish GoRest Report') {
                    steps {
                        publishHTML([
                            allowMissing: false,
                            alwaysLinkToLastBuild: false,
                            keepAll: true,
                            reportDir: 'newman',
                            reportFiles: 'GoRest*.html',
                            reportName: 'GoRest API Report',
                            reportTitles: ''
                        ])
                    }
                }
                stage('Publish Data driven Report') {
                    steps {
                        publishHTML([
                            allowMissing: false,
                            alwaysLinkToLastBuild: false,
                            keepAll: true,
                            reportDir: 'newman',
                            reportFiles: 'Datadriven.html',
                            reportName: 'Data driven API Report',
                            reportTitles: ''
                        ])
                    }
                }
            }
        }
    }
}