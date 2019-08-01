node {
    stage ('Checkout SCM'){
        git 'https://github.com/pkadam19/microservices-example.git'
    }
    stage ('compose up'){
        // Verify and remove if prev containers are present
        sh '''
           #!/bin/bash
           if [ $(docker ps -a | grep test2 | wc -l) -gt 0 ]
           then
               echo "Destroying prev. Container if it is already there"
               docker ps -a | grep test2 | awk '{print $1,$2 }'
               docker ps -a | grep test2 | awk '{print $1}' | xargs -I {} docker stop {}
               sleep 5
               docker ps -a | grep test2 | awk '{print $1}' | xargs -I {} docker rm {}
               echo "Removed older containers"
           else
               echo "Old Containers are not runninng"
          fi
        '''

        // Verify and remove if prev images are present
        sh '''
           #!/bin/bash
           if [ $(docker images | grep test2 | wc -l) -gt 0 ]
           then
               echo "Removing older images"
               docker images | grep test2 | awk '{print $1,$2,$3}'
               sleep 5
               docker images | grep test2 | awk '{print $3}' | xargs -I {} docker rmi {}
               echo "Removed Older images"
           else
               echo "Old images are not present"
          fi
        '''

        step([$class: 'DockerComposeBuilder', dockerComposeFile: 'docker-compose.yml', option: [$class: 'StartAllServices'], useCustomDockerComposeFile: true])
//        step([$class: 'DockerComposeBuilder', dockerComposeFile: 'docker-compose.yml', option: [$class: 'StartService', scale: 1, service: 'web'], useCustomDockerComposeFile: false])
        sh 'docker ps -l'
        sh 'docker images'
    }
    stage ('compose down'){
        step([$class: 'DockerComposeBuilder', dockerComposeFile: 'docker-compose.yml', option: [$class: 'StopAllServices'], useCustomDockerComposeFile: true])
    }
    stage ('Destroy onatiner and images') {
        sh '''
            docker ps -l
            docker ps -a | grep test2 | awk '{print $1,$2 }'
            docker ps -a | grep test2 | awk '{print $1}' | xargs -I {} docker stop {}
            sleep 2
            docker ps -a | grep test2 | awk '{print $1}' | xargs -I {} docker rm {}
        '''
        sh '''
           docker images
           docker images | grep test2 | awk '{print $1,$2,$3}'
           sleep 2
           docker images | grep test2 | awk '{print $3}' | xargs -I {} docker rmi {}
        '''
    }
}
