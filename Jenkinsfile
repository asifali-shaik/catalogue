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
    KEY = 'value'
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
        stage('npm install'){
            steps{
                script{
                    sh """
                        npm install 
                    """
                }
            }
        }
        stage('docker build'){
            steps{
                script{
                    sh """
                        docker build -t catalogue:$appversion .
                    """
                }
            }
        }
    }
}