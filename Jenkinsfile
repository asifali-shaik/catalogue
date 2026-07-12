pipeline{
    agent {
        node {
            label "roboshop"
        }
    }
    options{
        disableConcurrentBuilds() 
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