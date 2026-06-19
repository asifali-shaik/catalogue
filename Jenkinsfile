pipeline{
    agent{
        node {
            label "roboshop"
        }
        
    }
    options{
        timeout(time: 5, unit: 'MINUTES')
    }
    environment {
        appVersion = ""
        ACC_ID = "400392890477"
        region = "us-east-1"
    }

    stages{
        stage('Read version '){
            steps{
                script{
                    
                    def packageJson = readJSON file: 'package.json'
                         
                    appVersion = packageJson.version
                    echo "Building version ${appVersion}"
                    
                }
            }
        }
        stage('install dependencies '){
            steps{
                script{
                    sh """
                        /usr/bin/npm install

                    """
                }
            }
        }
        stage('build'){
            steps{
                script{
                    withAWS(credentials: 'aws-creds', region: 'us-east-1'){
                        sh """
                            aws ecr get-login-password --region ${region} | docker login --username AWS --password-stdin ${ACC_ID}.dkr.ecr.us-east-1.amazonaws.com
                            docker build -t ${ACC_ID}.dkr.ecr.${region}.amazonaws.com/roboshop/catalogue:${appVersion} .
                            docker push ${ACC_ID}.dkr.ecr.${region}.amazonaws.com/roboshop/catalogue:${appVersion}

                        """
                    }

                }
            }
        }

    }
}