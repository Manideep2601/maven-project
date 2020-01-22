pipeline {
    agent any
    stages{
        stage('branchname'){
            sh 'echo env.BRANCH_NAME'
        }
        stage('Build'){
            steps {
                sh 'mvn clean package'
            } 
            post {
                success {
                    echo 'Now Archiving...'
                    archiveArtifacts artifacts: '**/target/*.war'
                }
            }
        }
        stage ('OUTPUT'){
            steps {
                sh 'echo currentBuild.result'
            }
        }
    }
}
