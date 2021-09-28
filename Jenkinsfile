node('master') 
{
    stage('ContinuousDownload')
    {
        git 'https://github.com/intelliqittrainings/mavenabc.git'             
    }
    stage('ContinuousBuild')
    {
        sh 'mvn package'
    }
    stage('ContinuousDeployment')
    {
       deploy adapters: [tomcat9(credentialsId: '189a34cb-d927-4cac-b566-78fd44cea225', path: '', url: 'http://172.31.91.172:8080')], contextPath: 'qaapp', war: '**/*.war'
    }
    stage('ContinuousTesting')
    {
        git 'https://github.com/intelliqittrainings/FunctionalTesting.git'
        sh 'java -jar /home/ubuntu/.jenkins/workspace/ScriptedPipeline/testing.jar'
    }
    stage('ContinuousDelivery')
    {
       deploy adapters: [tomcat9(credentialsId: '189a34cb-d927-4cac-b566-78fd44cea225', path: '', url: 'http://172.31.86.48:8080')], contextPath: 'prodapp', war: '**/*.war'
    }
}
