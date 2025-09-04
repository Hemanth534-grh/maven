pipeline {
    agent any

    stages {
        stage('git checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/Hemanth534-grh/maven.git'
            }
        }
        stage('Maven Build') {
            steps {
                sh 'mvn clean package'
            }
        }
        stage('Tomcat deploy') {
            steps {
                sshagent(['tomcat9']) {
                sh "scp -o StrictHostKeyChecking=no target/*.war ec2-user@172.31.37.204:/home/ec2-user/tomcat9/webapps"
                sh "ssh ec2-user@172.31.37.204 /home/ec2-user/tomcat9/bin/shutdown.sh"
                sh "ssh ec2-user@172.31.37.204 /home/ec2-user/tomcat9/bin/startup.sh"
                }
            }
        }
    }
}
