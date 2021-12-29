pipeline {
    agent any
    stages{
        stage("cloning"){
            steps{
                git branch: 'main', url: 'https://github.com/hsreekanth/aws.git'
            }
        }
        stage("building"){
            steps{
                sh 'mvn clean install package'
            }
        }
        stage("Deploying into elasticbeanstalk"){
            steps{
       withCredentials([string(credentialsId: 'ACCESS_KEY', variable: 'ACCESS_KEY')]) {
           sh "/usr/local/bin/aws configure set aws_access_key_id ${ACCESS_KEY}"
       }
     withCredentials([string(credentialsId: 'SECRET_KEY', variable: 'SECRET_KEY')]) { 
            sh " /usr/local/bin/aws configure set aws_secret_access_key ${SECRET_KEY}"
        }
         sh '/usr/local/bin/aws configure set region ap-south-1'
         sh '/usr/local/bin/aws elasticbeanstalk update-environment --application-name tomcat --environment-name tomcat-env --version-label sampleapplication'
            }
        }
		
    }
}
