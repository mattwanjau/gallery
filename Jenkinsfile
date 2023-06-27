pipeline { 
    
  agent any
  tools{
      gradle 'Gradle'
  }

    environment {
        MY_LINK_RENDER = 'https://young-mountain-18198-00c30b751509.herokuapp.com'
        MY_LINK_HEROKU = ""
    }
  stages { 
      
        stage('clone repository') {
            
          steps { 
              
             echo "Cloning repository"
            git 'https://github.com/mattwanjau/gallery'
          }
        }
        stage('Build project'){
            
            steps{
                
                sh 'gradle build'
            }
        }
        stage('Tests'){
            
            steps{
                
                sh 'gradle Test'
            }
        }
        
        stage('Deploy to Heroku') {
  
            steps {
                //sh 'git push https://moringa:secretpassword@git.heroku.com/mattwanjau.git master'
                echo "Did not manage to deploy to Heroku"
                slackSend( message: " Could bot deploy to heroku. Linked to Render via Github .Render link: ${MY_LINK_RENDER}")
            }
        }
    }
    post {
        success {
            slackSend(message: "Gallery App deployment successful. Job Name - ${JOB_NAME} , Build number ${BUILD_NUMBER} , link ${MY_LINK_RENDER}")
        }

        failure {
            //emailext attachLog: true, body: 'See attached build log report', recipientProviders: [buildUser()], subject: "Job Name - ${JOB_NAME} , Build number ${BUILD_NUMBER}"
            slackSend( message: "Gallery App deployment faield. Job Name - ${JOB_NAME} , Build number ${BUILD_NUMBER}")
            slackSend( message: " Could not deploy to heroku. Linked to Render via Github .Render link: ${MY_LINK_RENDER}")
        }
    }
  }
