pipeline{
    agent any
    tools{
        maven "Maven"
    }
    stages{
        stage("scm checkout"){
            steps{
                checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[credentialsId: 'c5ef1406-f925-4e1f-9390-4462bbcffe14', url: 'https://github.com/Syedasara77/jenkins-cicd-demo.git']])
            }
        }
        stage("Build process"){
            steps{
                script{
                    bat 'mvn clean install'
                }
            }
        }
        stage("Deploy to container"){
            steps{
                deploy adapters: [tomcat9(credentialsId: 'tomcat-pwd', path: '', url: 'http://localhost:9090/')], contextPath: 'Jenkins-CI/CD', war: '**/*.war'
            }
        }
        }
        post{
            always{
               emailext attachLog: true, body: '''<html>
<body>
<p>Build Status : ${BUILD_STATUS}</p>
<p>Build Number : ${BUILD_NUMBER}</p>
<p>Check the <a href="${BUILD_URL}">Console output</a></p>
</body>
<html>''', mimeType: 'text/html', replyTo: 'sarasyeda777@gmail.com', subject: 'Pipeline Status : ${BUILD_NUMBER}', to: 'sarasyeda777@gmail.com'
            }
        }
}