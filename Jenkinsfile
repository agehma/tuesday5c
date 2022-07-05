pipeline
{
    agent any
    stages
    {
        stage('ContinuousDownload')
        {
            steps
            {
                git 'https://github.com/agehma/mavenproject.git'
            }
        }
        stage('continuousBuild')
        {
            steps
            {
                sh 'mvn package'
            }
        }
        stage('ContinuousDeployment')
        {
            steps
            {
                deploy adapters: [tomcat9(credentialsId: '3933de1f-781a-4384-bab7-5258db7fbfd3', path: '', url: 'http://172.31.85.178:8080')], contextPath: 'testapp', war: '**/*.war'
            }
        }
        stage('ContinuousTesting')
        {
            steps
            {
                git 'https://github.com/agehma/testingscript1.git'
                sh 'java -jar /var/lib/jenkins/workspace/Declarativepipeline-Postcon/testing.jar'
            }
        }
    }
    post
    {
        success
        {
            deploy adapters: [tomcat9(credentialsId: '3933de1f-781a-4384-bab7-5258db7fbfd3', path: '', url: 'http://172.31.85.56:8080')], contextPath: 'prodapp', war: '**/*.war'
        }
        failure
        {
            mail bcc: '', body: 'delivery into prodserver tomcat failed', cc: '', from: '', replyTo: '', subject: 'delivery failed', to: 'anongeric2001@gmail.com'
        }
    }
}

