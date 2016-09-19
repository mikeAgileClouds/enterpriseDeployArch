node ('swarm') {
    stage "Checkout Deployment Architecture and Operations Source"
    checkout scm
    
    stage "Checkout Developer Source Code"
    dir("${env.DEVPROJROOTDIR}") {
        git url: "${env.DEVPROJROOTURL}"
    }
    
    stage "Build Docker Images"
    dir("${env.DEVPROJCOMPOSEDIR}") {
        sh "docker-compose build --pull"
    }
    
    stage "Upload Docker Images to register"
    dir("${env.DEVPROJCOMPOSEDIR}") {
        sh "docker login -u ${env.DOCKERHUBUSER} -p ${env.DOCKERHUBPASSWD}"
        sh "docker-compose push"
    }
    
    stage "Create Application Bundle"
    dir("${env.DEVPROJCOMPOSEDIR}") {
        sh "docker-compose bundle -o demoapp.dab"
    }
    
    stage "Halt Deployed Services"
    dir("${env.DEVPROJCOMPOSEDIR}") {
        sh "docker node ls"
        // either rollin upgrade or remove/halt the stack
        // sh "docker-compose -f docker-compose.yml -f docker-compose.sd-label.yml down"
        // sh "docker-compose -p serv -f docker-compose.sd-launch.yml down"
    }

    stage "Deploy Birthday App"
    dir("${env.DEVPROJCOMPOSEDIR}") {
        sh "docker stack deploy demoapp"
    }
    
    stage "Scale Birthday App"
    dir("${env.DEVPROJCOMPOSEDIR}") {
        // sh "docker-compose -f docker-compose.yml -f docker-compose.sd-label.yml scale voting-app=3"
        // sh "docker-compose -f docker-compose.yml -f docker-compose.sd-label.yml scale result-app=2"
    }
    
    stage "Publish Birthday App details"
    dir("${env.DEVPROJCOMPOSEDIR}") {
        // sh "docker-compose -p serv -f docker-compose.sd-launch.yml ps"
        // sh "docker-compose ps"
    }
}
