pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/your-user/your-repo.git'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }

        stage('Deploy to Server') {
            steps {
                sh '''
                scp -o StrictHostKeyChecking=no target/*.war \
                ubuntu@SERVER_IP:/var/lib/tomcat9/webapps/

                ssh ubuntu@SERVER_IP "sudo systemctl restart tomcat9"
                '''
            }
        }
    }
}
