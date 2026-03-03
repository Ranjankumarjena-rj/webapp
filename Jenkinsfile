pipeline {

    agent any

    tools {
        jdk 'JAVA_HOME'
        maven 'M2_HOME'
    }

    environment {
        SERVER_IP = '13.232.170.2'
        TOMCAT_PATH = '/home/ec2-user/tomcat10/apache-tomcat-10.1.52'
    }

    stages {

        stage("Checkout") {
            steps {
                git branch: 'master',
                    url: 'https://github.com/Ranjankumarjena-rj/webapp'
            }
        }

        stage("Build") {
            steps {
                sh 'mvn clean package'
            }
        }

        stage("Deploy") {
            steps {
                sshagent(['tomcat']) {
                    sh """
                        scp -o StrictHostKeyChecking=no target/*.war ec2-user@$13.232.170.2:$/home/ec2-user/tomcat10/apache-tomcat-10.1.52/webapps/
                    """
                }
            }
        }
    }
}
