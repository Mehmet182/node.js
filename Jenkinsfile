pipeline {
    agent any

    environment {
        // Node.js sürümü
        NODEJS_VERSION = '18.x'
        // Uygulama dizini
        APP_DIR = '/home/ubuntu/hello-world-app'
    }

    tools {
        nodejs NODEJS_VERSION
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/Mehmet182/node.js.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }

        stage('Test') {
            steps {
                // Test komutlarınızı buraya ekleyebilirsiniz
                echo 'Test aşaması yok.'
            }
        }

        stage('Build') {
            steps {
                // Eğer derleme gerekiyorsa burada yapabilirsiniz
                echo 'Build aşaması yok.'
            }
        }

        stage('Deploy') {
            steps {
                sshagent(['your-ssh-key-id']) {
                    sh """
                        ssh -o StrictHostKeyChecking=no ubuntu@34.204.172.84 '
                            cd ${APP_DIR};
                            git pull origin main;
                            npm install;
                            pm2 restart hello-world-app || pm2 start app.js --name hello-world-app
                        '
                    """
                }
            }
        }
    }

    post {
        success {
            echo 'Deployment başarılı!'
        }
        failure {
            echo 'Deployment başarısız.'
        }
    }
}
