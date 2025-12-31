pipeline {
    agent {
        node {
            label 'AGENT-1'
        }
    }

    environment {
        COURSE = "Jenkins"
        appVersion = ""
        ACC_ID = "388779989110"
        PROJECT = "roboshop"
        COMPONENT = "catalogue"
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
        stage('Install Dependencies') {
            steps {
                script {
                    sh  """
                        npm install 
                    """
                }
            }
        }
        stage('Build Image') {
            steps {
                script {
                    withAWS(region:'us-east-1',credentials:'aws-creds') { 
                                                sh  """
                            aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin ${ACC_ID}.dkr.ecr.region.amazonaws.com
                            docker build -t ${ACC_ID}.dkr.ecr.us-east-1.amazonaws.com/${PROJECT}/${COMPONENT}:${appVersion} .
                            docker images
                            docker push ${ACC_ID}.dkr.ecr.us-east-1.amazonaws.com/${PROJECT}/${COMPONENT}:${appVersion}
                        """
                    }

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