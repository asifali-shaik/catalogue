pipeline{
    agent{
        node{
            label 'roboshop'
        }
    }
    options{
        timeout(time: 15, unit: 'MINUTES')
    }
    environment{
        appVersion = ""
    }
    stages{
        stage('read package.json-version'){
            steps{
                script{
                // Read the package.json file into an object
                 def packageJson = readJSON file: 'package.json'
                 appVersion = pacakgejson.version
        
                // Access properties directly
                echo "Building version: ${packageJson.version}"
        
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
        stage('building the docker image '){
            steps{
                script{
                    sh """

                        docker build -t catalogue:${appVersion} 
                    """
                }
            }
        }
    }
}