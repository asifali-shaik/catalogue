pipeline{
    agent {
        node {
            label "roboshop"
        }
    }
    envrionment{
        project = 'aws-project'
    }

    stages{
        stage('hello'){
            steps{
                script{
                    echo "hii jenkins"
                    echo $project
                }
            }

        }
    }
    post{
        always{
            echo 'happy !'
        }
        success{
            echo 'pipeline success !!'
        }
        failure{
            echo 'pipeline faliure !!!'
        }

    }
}