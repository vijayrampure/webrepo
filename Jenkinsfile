pipeline {
    agent any
   environment {
        PATH = "/opt/maven/bin:$PATH"
    }
    stages {
        stage('GitCloning') {
            steps {
                git branch: 'main', credentialsId: 'git_credentials', url: 'https://github.com/shashikanth-t/webrepo.git'
                echo 'Code Checkout done sucessfully.'
            }
			}
            stage('CodeBuild ') {
            steps {
            sh 'mvn clean install'
            echo 'Code build done sucessfully.'
            }
            }
            stage('CodeDeploy') {
            steps {
           sshagent(['deploy_user']) {
               
               sh "scp -o StrictHostKeyChecking=no webapp/target/webapp.war  ec2-user@34.207.89.215:/opt/apache-tomcat-9.0.80/webapps"
    
                            }         
            }
            }                 
        }
    }
