pipeline {
    agent any
    stages{
        stage('Build'){
            steps {
                echo env.BRANCH_NAME
                sh 'mvn clean package'
            }
            if( currentBuild.result == 'SUCCESS' )
            {
                // build ended early (ci skip)
                 echo("We win!")
                 return
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
