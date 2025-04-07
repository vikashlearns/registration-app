pipeline {
    agent { label 'Jenkins-Agent' }  // ✅ Correct agent syntax

    tools {
        jdk 'Java17'   // ✅ Ensure Java17 is correctly configured in Jenkins
        maven 'Maven3'  // ✅ Ensure Maven3 is correctly configured in Jenkins
    }

    stages {  // ✅ Fixed: 'stages' block should not take a parameter
        stage('Cleanup Workspace') {  // ✅ Correct syntax for defining a stage
            steps {
                cleanWs()
            }
        }

        stage('Checkout from SCM') {
            steps {
                git branch: 'main', 
                    credentialsId: 'github', 
                    url: 'https://github.com/V000ik/registration-app.git'
            }
        }

        stage('Build Application') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Test Application') {
            steps {
                sh 'mvn test'
            }
        }
        stage("SonarQube Analysis"){
            steps {
                script {
                    withSonarQubeEnv(credentialsId: 'jenkins-sonarqube-token') {
                        sh "mvn sonar:sonar"
                    }
                }
            }
        }
    }
    }
}
