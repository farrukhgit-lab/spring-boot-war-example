pipeline {
    agent any
    tools {
        maven 'Maven' 
    }
    stages {
        stage('Test') {
            steps {
                //mvn test
                sh 'mvn test'
            }
        }

        stage('Build') {
            steps {
                //mvn package
                sh 'mvn package'
               
            }
        }

        stage('Deploy on Test') {
            steps {
                // deploy on container -> plugin
                deploy adapters: [tomcat9(alternativeDeploymentContext: '', credentialsId: 'tomcat9details', path: '', url: 'http://192.168.34.8:8080')], contextPath: '/app', war: '**/*.war'
               
            }
        }
         stage('Deploy on Prod') {
            steps {
                // deploy on container -> plugin
                deploy adapters: [tomcat9(alternativeDeploymentContext: '', credentialsId: 'tomcat9details', path: '', url: 'http://192.168.34.9:8080')], contextPath: '/app', war: '**/*.war'
               
            }
        }
         
    }

    post {

        always {
            echo 'Pipeline Finished'
        }

        success {
            echo 'Build Successful'
        }

        failure {
            echo 'Build Failed'
        }
    }
}
