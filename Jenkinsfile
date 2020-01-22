pipeline {
    agent any
    stages{
        stage('Build'){
            steps {
                echo env.BRANCH_NAME
                sh 'mvn clean package'
            } 
            post {
                success {
                    echo 'Now Archiving...'
                    archiveArtifacts artifacts: '**/target/*.war'
                }
            }
        }
        stage ('Deploy to Staging'){
            steps {
                build job: 'Deploy-to-staging'
            }
        }
    }
}
