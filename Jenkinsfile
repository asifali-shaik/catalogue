pipeline{
    agent{
        node{
            label 'roboshop'
        }
    }
    environment{
        appVersion = ""
        ACC_ID = "400392890477"
    }
    stages{
        stage('read package.json-version'){
            steps{
                script{
                    def packageJson = readJSON file: 'package.json'
                    appVersion = packageJson.version
                    echo "Building version: ${appVersion}"
                }
            }
        }
        stage('install dependencies'){
            steps{
                script{
                    sh """
                        npm install
                    """
                }
            }
        }
        stage('sonarqube-scaner'){
            steps{
                script{
                    def scannerHome = tool 'sonar-8'   // name from Manage Jenkins → Tools → SonarQube Scanner installations
                    withSonarQubeEnv('sonar-server') {  // name from Manage Jenkins → System → SonarQube servers
                    sh "${scannerHome}/bin/sonar-scanner"
                 }
                }
            }
        }
        stage('building the docker image'){
            steps{
                script{
                    sh """
                        docker build -t catalogue:${appVersion} .
                    """
                }
            }
        }
        stage('push to ecr'){
            steps{
                script{
                    withAWS(credentials: 'AWS-CREDS', region: 'us-east-1'){
                        sh """
                            aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin ${ACC_ID}.dkr.ecr.us-east-1.amazonaws.com
                            docker tag catalogue:${appVersion} ${ACC_ID}.dkr.ecr.us-east-1.amazonaws.com/roboshop/catalogue:${appVersion}
                            docker push ${ACC_ID}.dkr.ecr.us-east-1.amazonaws.com/roboshop/catalogue:${appVersion}
                        """
                    }
                }
            }
        }
    }
}

