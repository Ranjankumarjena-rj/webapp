pipeline{
 tools{
        jdk 'JAVA_HOME'
        maven 'M2_HOME'
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
		  
      stage("deploy"){
	    steps{
		 
        sshagent(['docker-slave]) {
    
   
        sh """
                 
            scp -o StrictHostKeyChecking=no target/myweb.war ec2-user@13.233.87.35:/home/ec2-user/tomcat10/apache-tomcat-10.1.52/webapps/

              ssh ec2-user@13.233.87.35 /home/ec2-user/tomcat10/apache-tomcat-10.1.52/bin/shutdown.sh
              ssh ec2-user@13.233.87.35 /home/ec2-user/tomcat10/apache-tomcat-10.1.52/bin/startup.sh
            
          
          """



    // some block
}
		}
		}
	  }
	}
