node {
    stage ('compose up'){
//        step([$class: 'DockerComposeBuilder', dockerComposeFile: 'docker-compose.yml', option: [$class: 'StartAllServices'], useCustomDockerComposeFile: true])
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
