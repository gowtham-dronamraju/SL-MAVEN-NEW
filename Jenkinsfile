pipeline {
    agent any

    environment {
        TOMCAT_USER = 'tomcat'
        TOMCAT_PASSWORD = 'admin_password'
        TOMCAT_HOST = '127.0.0.1'
        TOMCAT_PORT = '8080'
        TOMCAT_WEBAPPS_DIR = '/opt/tomcat/webapps'
        LOCAL_JAR_PATH = '/var/lib/jenkins/.m2/repository/devops/sl/devops.sl/0.0.1-SNAPSHOT/devops.sl-0.0.1-SNAPSHOT.jar'
        REMOTE_JAR_PATH = '/opt/tomcat/webapps/devops.sl-0.0.1-SNAPSHOT.jar'
        SSH_KEY_PATH = '/var/lib/jenkins/.ssh/id_rsa'
        SSH_USER = 'gowtham'
        SSH_PASSWORD = 'Avyaan1!'
    }
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
            
        


        stage('Deploy JAR to Tomcat') {
            steps {
                script {
                    // Deploy the JAR file using SSH and SCP
                    sh '''
                    # Check if the SSH key has the right permissions
                    chmod 600 $SSH_KEY_PATH

                    # Transfer the JAR file to the Tomcat server
                    scp -i $SSH_KEY_PATH $LOCAL_JAR_PATH $TOMCAT_USER@$TOMCAT_HOST:$REMOTE_JAR_PATH
                    
                    # Restart Tomcat to apply changes (only if needed)
                    ssh -i $SSH_KEY_PATH $TOMCAT_USER@$TOMCAT_HOST "sudo systemctl restart tomcat"
                    '''
                }
            }
        }
    }

    post {
        success {
            echo 'Deployment was successful!'
        }
        failure {
            echo 'Deployment failed.'
        }
    }    

   
}
