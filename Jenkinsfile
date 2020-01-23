pipeline {
    agent any
    stages{
      stage("Checkout")
      {
        steps {
         script {
           dir('repo') {
             scm_vars = checkout scm
             //setCommitterInfo(scm_vars.GIT_COMMITTER_NAME, scm_vars.GIT_COMMITTER_EMAIL)
             env.GIT_BRANCH= scm_vars.GIT_BRANCH.tokenize('/')[1]
             env.REPO = scm_vars.GIT_URL.tokenize('/')[3].split("\\.")[0]
	   }
         }
        }
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
    
        stage('Output'){
            steps {
                echo 'Hello World'
                sh 'echo $GIT_BRANCH'
	        sh 'echo $REPO'
	        echo "RESULT:${currentBuld.result}"
            }
        }
      }	    
}
