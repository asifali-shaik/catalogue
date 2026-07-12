pipeline{
    agent {
        node {
            label "roboshop"
        }
    }
    stages{
        stage('hello'){
            steps{
                script{
                    echo "hii jenkins"
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