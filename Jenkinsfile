pipeline{
 tools{
        jdk 'JAVA_HOME_DOCKER'
        maven 'M2_HOME_DOCKER'
    }
     agent any
	  
	  stages{
	  
	  stage("checkout"){
	   steps{
	   git 'https://github.com/Ranjankumarjena-rj/webapp.git'
	   }
	                  }
	
	   stage("compile"){
	    steps{
		 sh 'mvn compile'
		}
		}
       stage("test"){
	    steps{
		 sh 'mvn test'
		}
		}
       stage("package"){
	    steps{
		 sh 'mvn clean package'
                 sh "mv target/*.war target/myweb.war"

		}
		}
		  
      stage("docker_node"){
	    steps{
		 
        sshagent(['docker_agent]) {
    
   
        sh """
                 
            scp -o StrictHostKeyChecking=no target/myweb.war ec2-user@3.110.133.13:/usr/local/tomcat/webapps/

              ssh ec2-user@3.110.133.13 /usr/local/tomcat/bin/shutdown.sh
              ssh ec2-user@3.110.133.13 /usr/local/tomcat/bin/startup.sh
            
          
          """



    // some block
}
		}
		}
	  }
	}
