pipeline{

    agent any
    tools{
        gradle "gradle"
    }
    stages{

        stage("SCM checkout"){
            steps{
                checkout scmGit(branches: [[name: '*/main']],
                extensions: [], userRemoteConfigs: [[url: 'https://github.com/thejavaengineer/jenkins.git']])
            }
        }

        stage("Build Process"){
            steps{
                script{
                    bat 'gradle clean build'
                }
            }
        }

        stage("Deploy to Container"){
            steps{
                deploy adapters: [
                        tomcat9(
                            credentialsId: 'tomcat-pwd',
                            path: '',
                            url: 'http://localhost:9090/')],
                contextPath: 'jenkins',
                war: '**/.war'
            }
        }

    }
}