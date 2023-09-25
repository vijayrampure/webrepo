pipeline {
    agent any
       environment {
        PATH = "/opt/maven/bin:$PATH"
    }
    stages {
        stage('GitCloning') {
            steps {
                git branch: 'main', credentialsId: 'git_credential', url: 'https://github.com/vijayrampure/webrepo.git'
                echo 'Code Checkout done sucessfully.'
            }
			}
            stage('CodeBuild') {
            steps {
                    sh 'mvn clean package'
                    echo 'Code build done sucessfully.'
            }
            }
            stage('CodeDeploy') {
            steps {
           sshagent(['deploy_user']) {
               
               sh "scp -o StrictHostKeyChecking=no /var/lib/jenkins/workspace/pjob-2/webapp/target/webapp.war  ec2-user@3.15.146.181:/opt/apache-tomcat-9.0.80/webapps"
    
                            }         
            }
            }            
        }
    }
