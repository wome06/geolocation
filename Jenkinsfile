pipeline{
    agent any
    tools {
        maven 'M2_HOME'
    }
    stages{
        stage('maven built'){
            steps{
                sh 'mvn clean install package'
            }
            
        }
        stage('check pwd'){
            steps{
                sh 'pwd'
            }
            
        }
        stage('list directory'){
            steps{
                sh 'ls'
            }
            
        }
    }
}