pipeline {
    agent any
    tools {        
        maven 'MAVEN_HOME'
    }

    stages {

        stage('Welcome Stage') {
            steps {
                echo "Welcome to Pipeline"
            }
        }  
        stage('Maven Test') {
            steps {
                sh 'mvn test'
            }
        }      

        stage('Maven Build') {
            steps {
                sh 'mvn clean install'
            }
        }        
        stage('Build Success') {
            steps {
                echo "Build Successful"
            }
        }   
        
        stage('Final Success') {
            steps {
                echo "Final Successful"
            }
        }     
        stage('Deploy to Tomcat') {
            steps {
                script {
                    // Define your Tomcat server details
                    def tomcatServer = '127.0.0.1'  // Replace with your Tomcat server's address
                    def tomcatUser = 'gowtham'    // Replace with your Tomcat username
                    def tomcatPassword = 'Avyaan1!' // Replace with your Tomcat password
                    def tomcatPath = 'admin@127.0.0.1:/opt/tomcat/webapps' // Path to Tomcat's webapps folder
                    
                    // Define the JAR path to deploy
                    def jarFile = '/var/lib/jenkins/.m2/repository/devops/sl/devops.sl/0.0.1-SNAPSHOT/devops.sl-0.0.1-SNAPSHOT.jar'

                    // Use SSH to copy the JAR file to Tomcat's webapps directory
                    sh """
                        scp -o StrictHostKeyChecking=no -i /home/gowtham/.ssh/id_rsa ${jarFile} ${tomcatUser}@${tomcatServer}:${tomcatPath}
                    """
                }
            }
        }    

    }
}
