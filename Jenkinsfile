pipeline {
   agent any

   tools {
      maven "maven3"
   }

   stages {
      stage('Build') {
         steps {
            git credentialsId: 'github_credentials', url: 'https://github.com/jmstechhome16/spring-petclinic.git'

            sh "mvn package"
         }
        post {
            success {
               junit '**/target/surefire-reports/TEST-*.xml'
               archiveArtifacts 'target/*.war'
            }
			}

      }

    stage ('success'){
            steps {
                script {
                    currentBuild.result = 'SUCCESS'
                }
            }
        }
    }

    post {
        failure {
            script {
                currentBuild.result = 'FAILURE'
            }
        }

        always {
            step([$class: 'Mailer',
                notifyEveryUnstableBuild: true,
                recipients: "jmstechhome16@gmail.com",
                sendToIndividuals: true])
        }
    }
}
