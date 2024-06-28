pipeline {
    agent {
        docker {
            image 'maven:3.9.2'
            args '-v /root/.m2:/home/maven/.m2'
        }
    }
    stages {
        stage('Build') {
            steps {
                sh 'mvn -B -DskipTests -Dmaven.repo.local=/home/maven/.m2/repository clean package'
            }
        }
        stage('Test') {
            steps {
                sh 'mvn -Dmaven.repo.local=/home/maven/.m2/repository test'
            }
            post {
                always {
                    junit 'target/surefire-reports/*.xml'
                }
            }
        }
        stage('Deliver') {
            steps {
                sh './jenkins/scripts/deliver.sh'
            }
        }
    }
}
