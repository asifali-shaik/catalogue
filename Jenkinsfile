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
        stage('docker build'){
            steps{
                script{
                    sh """
                        docker build -t catalogue:$appVersion .
                    """
                }
            }
        }
    }
}