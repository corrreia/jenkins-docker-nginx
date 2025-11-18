pipeline {
agent any
environment {
IMAGE_NAME = "corrreia/jenkins-docker-nginx"
IMAGE_TAG = "latest"
CONTAINER_NAME = "correia-nginx-app"
}
stages {
stage('Build Docker Image') {
steps {
script {
// Constrói a imagem e guarda numa variável Groovy
customImage = docker.build("${IMAGE_NAME}:${IMAGE_TAG}")
}
}
}
stage('Run Container Locally') {
steps {
script {
sh "docker run --rm -d --name ${CONTAINER_NAME} -p 8081:80 ${IMAGE_NAME}:${IMAGE_TAG}"
echo "Aceda a http://localhost:8081"
}
}
}
stage('Push Docker Image to Docker Hub') {
steps {
script {
docker.withRegistry('https://index.docker.io/v1/', 'my-docker-token') {
customImage.push()
}
}
}
}
}
post {
always {
sh 'docker container prune -f || true'
sh 'docker image prune -f || true'
}
}
}
