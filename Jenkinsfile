pipeline
{   
    agent any
    stages{
        stage("cont_download")
        {
            steps{
                    git branch: 'main', url: 'https://github.com/nocturnaldevops/Project1.git'
            }
        }
        stage("cont_build")
        {
            steps{
                sh 'mvn package'
            }
        }
        stage("cont_deploy_to_test")
        {
            steps{
                deploy adapters: [tomcat9(credentialsId: '03427832-f55c-4d09-b70f-1e24db73b53a', path: '', url: 'http://172.31.9.150:8080')], contextPath: 'test1', war: '**/*.war'
            }
        }
        stage("cont_test")
        {
            steps{
                    mail bcc: '', body: '''Dear Test team,
                    please test the application deployed on to test server on this url
                    http://35.154.20.135:8080/test1''', cc: '', from: '', replyTo: '', subject: 'test the application', to: 'sonijadhav1235@gmail.com'
                }
        }
        stage("cont_delivery")
        {
            steps{
                    deploy adapters: [tomcat9(credentialsId: '6d7ce63a-7194-418d-a702-34ced291211b', path: '', url: 'http://172.31.5.193:8080')], contextPath: 'rel1', war: '**/*.war'
                    mail bcc: '', body: '''The application is live on 
                    http://43.204.114.201:8080/rel1''', cc: '', from: '', replyTo: '', subject: 'Application is LIVE', to: 'sonijadhav1235@gmail.com'
            }
        }
    }
}
