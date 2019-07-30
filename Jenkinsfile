node {
    stage ('Checkout SCM'){
        git 'https://github.com/pkadam19/microservices-example.git'
    }
    stage ('compose up'){
        step([$class: 'DockerComposeBuilder', dockerComposeFile: 'docker-compose.yml', option: [$class: 'StartService', scale: 1, service: 'web'], useCustomDockerComposeFile: false])
        sh 'docker ps -l'
        sh 'docker images'
    }
    stage ('compose down'){
        step([$class: 'DockerComposeBuilder', dockerComposeFile: 'docker-compose.yml', option: [$class: 'StopAllServices'], useCustomDockerComposeFile: false])
        sh 'docker ps -l'
        sh 'docker images'
    }
}
