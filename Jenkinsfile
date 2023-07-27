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
                  sh 'mvn sonar:sonar -Dsonar.projectKey=wome06_geolocation -Dsonar.java.binaries=.'
              }
            }
          }
        stage('Check Quality Gate') {
            steps {
                echo 'Checking quality gate...'
                script {
                    timeout(time: 20, unit: 'MINUTES') {
                        def qg = waitForQualityGate()
                        if (qg.status != 'OK') {
                            error "Pipeline stopped because of quality gate status: ${qg.status}"
                        }
                    }
                }
            }
        }
        
         
        stage('maven package') {
            steps {
                sh 'mvn clean'
                sh 'mvn install -DsKipTests'
                sh 'mvn package -DsKipTests'
            }
        }
        
        stage('Deploy image') {      
            steps{
                echo 'deployment'
                
            }
        }    
         
         
    }
}