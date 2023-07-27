pipeline {
    triggers {
  pollSCM('* * * * *')
    }
   agent {
      docker { image 'maven:amazoncorretto' }
   }
    tools {
  maven 'M2_HOME'
}


    stages {
        stage("build & SonarQube analysis") {
            agent any
            steps {
              withSonarQubeEnv('SonarServer') {
                  sh 'mvn sonar:sonar'
              }
            }
          }
        
         
        stage('maven package') {
            steps {
                sh 'mvn clean'
                sh 'mvn install'
                sh 'mvn package'
            }
        }
        stage('test') {
            
            steps {
               sh 'mvn test'
            }
        }
        stage('Deploy image') {      
            steps{
                echo 'deployment'
                
            }
        }    
         
         
    }
}