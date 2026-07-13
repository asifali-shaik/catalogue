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
                    // Read the package.json file into an object
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
                            aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin 
                            ${ACC_ID}.dkr.ecr.us-east-1.amazonaws.com
                            docker build -t  ${ACC_ID}.dkr.ecr.us-east-1.amazonaws.com/roboshop/catalogue:${appVersion}.
                            docker push ${ACC_ID}.dkr.ecr.us-east-1.amazonaws.com/roboshop/catalogue:${appVersion}
                        """
                    }
                }
            }
        }
 
    }
}
    
