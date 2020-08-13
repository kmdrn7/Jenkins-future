pipeline {
    agent {
        label "dockerworker"
    }
    stages {
        stage('Build') {
            steps {
                sh 'mvn -B -DskipTests clean package'
            }
        }
        stage('Test') {
            steps {
                sh 'mvn test'
            }
            post {
                always {
                    junit 'target/surefire-reports/*.xml'
                }
            }
        }
        stage('Build image') {
            steps {
                sh 'sudo docker build -t my-app .'
            }
        }
        stage('Run app') {
            steps {
                sh 'sudo docker run my-app'
            }
        }
    }
    post {
        always {
            deleteDir()
        }
    }
}
