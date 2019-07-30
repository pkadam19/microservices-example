node {
    stage ('checkout'){
        sh 'git clone https://github.com/pkadam19/microservices-example.git'
    }
    stage ('compose up'){
        sh 'docker-compose up -d'
        sh 'docker ps -l'
        sh 'docker images'
    }
    stage ('compose down'){
        sh 'docker-compose down'
        sh 'docker ps -l'
        sh 'docker images'        
    }
}
