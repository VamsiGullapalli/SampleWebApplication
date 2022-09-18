pipeline {
    agent any
    parameters {
        string(name: 'TomcatURL', defaultValue: 'http://44.204.6.196:8080/', description: 'What is the tomcat IP?')
        string(name: 'contextpath', defaultValue: 'sampleapp-dev', description: 'What is the context pat?')
    }
    tools {

        maven "maven-3.8"
    }

    stages {
        stage('SCM-checckout') {
            steps {

                git 'https://github.com/VamsiGullapalli/SampleWebApplication.git'
                
            }
        }
        stage('Maven-Build') {
            steps {
                
                sh "mvn -v"
                sh "mvn clean package"
            }
        }  
        stage('test-cases') {
            steps {
                echo 'testing'
            }
        }
        stage('deploy') {
            steps {
                echo "deploying to Tomcat URL"
                echo "${params.TomcatURL}"
                echo "${params.contextpath}"
                input ''
                echo "${params.TomcatURL}/${params.contextpath}"
                emailext body: 'approve', recipientProviders: [requestor()], subject: 'build status', to: 'learndevops202201@gmail.com'
                
            }
        }     
        stage('deploy') {
            steps {
                echo "deploying to Tomcat URL"
                echo "${params.TomcatURL}"
                echo "${params.contextpath}"
                input ''
                deploy adapters: [tomcat9(credentialsId: 'tomcat-deploy', path: '', url: "${params.TomcatURL}")], contextPath: "${params.contextpath}", onFailure: false, war: '**/*.war'
                echo 'URL to access application is' 
                echo "${params.TomcatURL}/${params.contextpath}"
            }
        }               
    }
}
