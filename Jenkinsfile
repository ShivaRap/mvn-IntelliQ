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
                deploy adapters: [tomcat9(credentialsId: 'a39edb98-a434-4134-afc0-81cc9b30fd62', path: '', url: 'http://172.31.30.169:8080')], contextPath: 'testapp2', war: '**/*.war'
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
                deploy adapters: [tomcat9(credentialsId: 'a39edb98-a434-4134-afc0-81cc9b30fd62', path: '', url: 'http://172.31.26.237:8080')], contextPath: 'prodapp2', war: '**/*.war'
            }
        }
    }
}
