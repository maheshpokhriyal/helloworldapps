pipeline {
    agent { label 'main' }
    stages {
        stage('Clone sources') {
            steps {
                git branch: 'feature/mycode', credentialsId: 'github', url: 'https://github.com/maheshpokhriyal/helloworldapps.git'
            }
        }
		
		stage('Delete artifacts') {
            steps {
                sh "rm -fr ${WORKSPACE}/target"
            }
        }
       

        stage ("Maven Build") {
          environment {
            MAVEN_HOME = tool 'maven3.6' // this is the name of maven configured on global configuration tool
          }        
          steps {
             configFileProvider([configFile(fileId: '0801f489-05ab-4a46-8f86-db2fe12eba87', variable: 'MAVEN_SETTINGS_XML')]) {
             tool name: 'maven3.6', type: 'maven'
             sh "${MAVEN_HOME}/bin/mvn -s $MAVEN_SETTINGS_XML install clean deploy"
             } 
          }     
              
        }
		
		stage('list artifacts') {
            steps {
			    sh "ls -ltr ${WORKSPACE}"
                sh "ls -ltr ${WORKSPACE}/target"
            }
        }
               
 
		stage('deploy artifacts') {
            steps {
			    sh "cp ${WORKSPACE}/target/helloworldapps-1.0-SNAPSHOT.war /usr/local/package/apache-tomcat-9.0.65/webapps/helloworldapps.war"
                sh "ls -ltr /usr/local/package/apache-tomcat-9.0.65/webapps/"
            }
        }        
     
        
    }
  
  
} 