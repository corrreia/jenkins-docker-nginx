pipeline {
agent any
stages {
stage('Build Docker Image') {
steps {
script {
docker.build('jenkins-docker-nginx:latest')
}
}
}
stage('Run Container') {
steps {
sh 'docker run --rm -d --name correia-nginx-app -p 8081:80 jenkins-docker-nginx:latest'
echo "Aceda a http://localhost:8081 para ver a página"
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
