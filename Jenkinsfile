pipeline
{
    agent any
    stages
    {
        stage('ContinuousDownload')
        {
            steps
            {
                git 'https://github.com/agehma/tuesday5c.git'
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
       
    }
}

