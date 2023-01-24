pipeline
{
    agent any
    stages
    {
        stage('ContinuousDownload')
        {
            steps
            {
                git 'https://github.com/ShivaRap/mvn-IntelliQ.git'
            }
        }
        stage('ContinuousBuild')
        {
            steps
            {
                sh '''mvn package'''
            }
        }
        stage('ContinuousDeployment')
        {
            steps
            {
                sh 'scp /var/lib/jenkins/workspace/DeclarativePipeline1/webapp/target/webapp.war ubuntu@172.31.20.165:/var/lib/tomcat9/webapps/testapp3.war'
            }
        }
        stage('ContinuousTesting')
        {
            steps
            {
                git 'https://github.com/intelliqittrainings/FunctionalTesting.git'
                sh 'java -jar /var/lib/jenkins/workspace/DeclarativePipeline1/testing.jar'
            }
        }
        stage('ContinuousDelivery')
        {
            steps
            {
                input message: 'waiting for approval from DM', submitter: 'Bruce'
                sh 'scp /var/lib/jenkins/workspace/DeclarativePipeline1/webapp/target/webapp.war ubuntu@172.31.26.237:/var/lib/tomcat9/webapps/prodapp3.war'
            }
        }
    }
}
