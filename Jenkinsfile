pipeline {
    agent any

    tools {
        maven 'Maven 3'   // You must configure this tool in Jenkins
        jdk 'JDK 21'      // You must configure this tool in Jenkins
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Archive WAR') {
            steps {
                archiveArtifacts artifacts: 'target/*.war', fingerprint: true
            }
        }

       stage('Deploy to Tomcat') {
            steps {
                sh '''
                    sudo cp target/sample-war.war /opt/tomcat/webapps/
                    sudo chown tomcat:tomcat /opt/tomcat/webapps/sample-war.war
                    sudo systemctl restart tomcat
                '''
            }
        }
    }
}

