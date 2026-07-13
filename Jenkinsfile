pipeline{
    agent{
        node{
            label 'roboshop'
        }
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
    }
}