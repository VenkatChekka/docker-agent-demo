pipeline {
    
   agent any

    tools {
      maven 'maven'
    }
    
    
    stages{
        stage ('Checkout') {
            steps{
                checkout poll: false, scm: scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/VenkatChekka/docker-agent-demo.git']])
            }
            
        }
        stage ('Build') {
             agent {
            label "agentnode2"
          }
            steps {
                echo "Build Stage is in progress"
                sh 'mvn compile'
            }
            
        }
        stage ('Test'){
             agent {
            label "agentnode2"
          }
            steps {
                echo "Test Stage is in progress"
                sh 'mvn test'
                junit 'target/surefire-reports/*.xml'
            }
            
        }
        stage('Deploy'){
             agent {
            label "agentnode2"
          }
            input {
              message 'Do you want to deploy build?'
              ok 'Yes I want'
              parameters {
                string description: 'Who is Approver?', name: 'Approver'
              }
            }
            steps{
                echo 'Deploying Build'
            }
        }
    }
}
