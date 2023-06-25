pipeline { 
    
  agent any
  tools{
      gradle 'Gradle'
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
              }
}
    }
  }
