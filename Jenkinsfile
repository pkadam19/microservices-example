node {
    stage ('compose up'){
        step([$class: 'DockerComposeBuilder', dockerComposeFile: 'docker-compose.yml', option: [$class: 'StartAllServices'], useCustomDockerComposeFile: true])
        sh 'docker ps -l'
        sh 'docker images'
    }
    stage ('compose down'){
        step([$class: 'DockerComposeBuilder', dockerComposeFile: 'docker-compose.yml', option: [$class: 'StopAllServices'], useCustomDockerComposeFile: true])
        sh 'docker ps -l'
        sh 'docker images'        
    }
}
