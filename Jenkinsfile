pipeline { 
    
  agent any
  tools{
      nodejs "20.3.1"
  }

    environment {
        MY_LINK_RENDER = 'https://moringaweek2ip1.onrender.com'
        MY_LINK_HEROKU = ""
    }
  stages { 
      
        stage('clone repository') {
            
          steps { 
              
             echo "Cloning repository"
            git 'https://github.com/mattwanjau/gallery'
          }
        }
        stage('Install'){
            
            steps{
                
                sh 'npm install'
            }
        }
        stage('Tests'){
            
            steps{
                sh 'npm run test'
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
