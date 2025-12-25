pipeline {
    agent {
        node {
            label 'AGENT-1'
        }
    }

    environment {
        COURSE = "Jenkins"
        appVersion = ""
    }

    options {
        // Timeout counter starts AFTER agent is allocated
        timeout(time: 10, unit: 'HOURS')
        disableConcurrentBuilds()
    }

    stages {
        stage('Read Version') {
            steps {
                script {
                    def packageJSON = readJSON file: 'package.json' // package.json inside the content assign to packageJson variable then we retrive the version
                    appVersion = packageJSON.version
                    echo "appVersion is : ${appVersion}"

                }
            }
        }
        stage('Test') {
            steps {
                script {
                    sh  """
                        echo "Testing"
                    """
                }
            }
        }
        stage('Deploy') {
      /*       input {
                message "Should we continue?"
                ok "Yes, we should."
                submitter "alice,bob"
                parameters {
                    string(name: 'PERSON', defaultValue: 'Mr Jenkins', description: 'Who should I say hello to?')
                }
            } */
            when { 
                expression { "$params.DEPLOY" == "true" } 
            }
            steps {
                script {
                    sh  """
                        echo "Deploying"
                    """
                }
            }
        } 
    } 
    post {
        always {
            echo "pipeline running always"
        }
        success {
            echo "if success"
        }
        failure {
            echo "if failure"
        }
        aborted {
            echo "aborted"
        }
    }
}