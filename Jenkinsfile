node {
    stage ('Checkout SCM'){
        git 'https://github.com/pkadam19/microservices-example.git'
    }
    stage ('compose up'){
        sh '''
           // Verify and remove if prev containers are present
           #!/bin/bash
           if [ $(docker ps -a | grep test2 | wc -l) -gt 0 ]
           then
               echo "Destroying prev. Container if it is already there"
               docker ps -a
               docker stop $(docker ps -a | grep test2)
               sleep 5
               docker rm $(docker ps -a | grep test2)
               echo "Removed older containers"
           else
               echo "Old Container is not runninng"
          fi
        '''

        // Verify and remove if prev images are present
        sh '''
           #!/bin/bash
           if [ $(docker images | grep test2 | wc -l) -gt 0 ]
           then
               echo "Removing older images"
               docker images
               docker images $(docker ps  | grep test2)
               sleep 5
               docker rmi $(docker images | grep test2)
               echo "Removed Older images"
           else
               echo "Old Container is not runninng"
          fi
        '''

        step([$class: 'DockerComposeBuilder', dockerComposeFile: 'docker-compose.yml', option: [$class: 'StartAllServices'], useCustomDockerComposeFile: true])
//        step([$class: 'DockerComposeBuilder', dockerComposeFile: 'docker-compose.yml', option: [$class: 'StartService', scale: 1, service: 'web'], useCustomDockerComposeFile: false])
        sh 'docker ps -l'
        sh 'docker images'
    }
    stage ('compose down'){
//        step([$class: 'DockerComposeBuilder', dockerComposeFile: 'docker-compose.yml', option: [$class: 'StopAllServices'], useCustomDockerComposeFile: true])
        sh 'docker ps -a'
        sh 'docker images'
    }
}
