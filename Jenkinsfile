pipeline
{
    agent any
    stages
    {
        stage('continuousdownload')
        {
           steps
           {
              git 'https://github.com/intelliqittrainings/maven.git'
           }
        }
        stage('continuousbuild')
        {
            steps
            {
                sh '''mvn package'''
            }
        }
        stage('continuousdeployment')
        {
            steps
            {
                deploy adapters: [tomcat9(credentialsId: '773fb35d-6b0b-4a82-8d35-14aef633bacd', path: '', url: 'http://172.31.12.240:8080')], contextPath: 'test1', war: '**/*.war'
            }
        }
        stage('continuoustesting')
        {
            steps
            {
                git 'https://github.com/intelliqittrainings/FunctionalTesting.git'
                sh '''java -jar /var/lib/jenkins/workspace/DeclarativePipeline1/testing.jar'''
            }
        }
        stage('continuousdelivery')
        {
            steps
            {
                deploy adapters: [tomcat9(credentialsId: '773fb35d-6b0b-4a82-8d35-14aef633bacd', path: '', url: 'http://172.31.1.52:8080')], contextPath: 'prod1', war: '**/*.war'
            }
        }
    
    }
}
