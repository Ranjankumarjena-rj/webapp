pipeline {
    agent any

    tools {
        jdk 'JAVA_HOME_DOCKER'
        maven 'M2_HOME_DOCKER'
    }

    stages {
        stage("Checkout") {
            steps {
                git 'https://github.com/Ranjankumarjena-rj/webapp.git'
            }
        }

        stage("Compile") {
            steps {
                sh 'mvn compile'
            }
        }

        stage("Test") {
            steps {
                sh 'mvn test'
            }
        }

        stage("Package") {
            steps {
                sh 'mvn package -DskipTests' 
                sh 'mv target/*.war target/myweb.war'
            }
        }

        stage("Deploy to Tomcat") {
            steps {
                sshagent(['docker_node']) {
                    sh """
                        scp -o StrictHostKeyChecking=no target/myweb.war ec2-user@3.110.133.13:/usr/local/tomcat/webapps/
                        ssh -o StrictHostKeyChecking=no ec2-user@3.110.133.13 "/usr/local/tomcat/bin/shutdown.sh"
                        ssh -o StrictHostKeyChecking=no ec2-user@3.110.133.13 "/usr/local/tomcat/bin/startup.sh"
                    """
                }
            }
        }
    }
}
