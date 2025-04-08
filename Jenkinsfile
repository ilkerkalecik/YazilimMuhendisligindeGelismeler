pipeline {
    agent any 
    triggers {
        githubPush()
    }
    environment {
        PATH = "/usr/local/bin:/usr/bin:/bin:/usr/sbin:/sbin"
        IMAGE_NAME = "test-image"
        CONTAINER_NAME = "test-container"
    }
    stages {
        stage('Repo Klonla') {
            steps {
                git url: 'https://github.com/ilkerkalecik/YazilimMuhendisligindeGelismeler.git', branch: 'main'
            }
        }
        stage('Docker Image Oluştur') {
            steps {
                sh "docker build -t ${IMAGE_NAME} ."
            }
        }
        stage('Eski Conteyneri Durdur') {
            steps {
                sh "docker rm -f ${CONTAINER_NAME} || true"
            }
        }
        stage('Yeni Conteyneri Oluştur') {
            steps {
                sh "docker run -d --name ${CONTAINER_NAME} -p 5050:80 ${IMAGE_NAME}"
            }
        }
    }
    post {
        success {
            echo "Yayın Başarılı"
        }
        failure {
            echo "Başarısız"
        }
    }
}
