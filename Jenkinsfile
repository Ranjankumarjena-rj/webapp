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
                sh 'mv target/idream-it-solutions.war target/myweb.war'
            }
        }
        stage("Deploy to Tomcat") {
            steps {
                sshagent(['docker_agent']) {
                    sh """
                        scp -o StrictHostKeyChecking=no target/myweb.war ec2-user@15.206.166.58:/tmp/myweb.war
                        ssh -o StrictHostKeyChecking=no ec2-user@15.206.166.58 "docker cp /tmp/myweb.war tomcat:/usr/local/tomcat/webapps/"
                        ssh -o StrictHostKeyChecking=no ec2-user@15.206.166.58 "docker restart tomcat"
                    """
                }
            }
        }
    }
}
