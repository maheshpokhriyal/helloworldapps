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
             configFileProvider([configFile(fileId: '135f47ea-dde5-47cc-898f-9d1c498b42eb', variable: 'MAVEN_SETTINGS_XML')]) {
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
			    sh "cp ${WORKSPACE}/target/helloworldapp-1.0-SNAPSHOT.war /apps/tomcat/tomcat/webapps/helloworldapp.war"
                sh "ls -ltr /apps/tomcat/tomcat/webapps/"
            }
        }        
     
        
    }
  
  
} 