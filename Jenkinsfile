node ('swarm') {
    stage "Checkout Deployment Architecture and Operations Source"
    checkout scm
    
    stage "Checkout Developer Source Code"
    dir("${env.DEVPROJROOTDIR}") {
        git url: "${env.DEVPROJROOTURL}"
    }
    
    stage "Configure Deployment Environment"
    sh "docker service ls"
    // sh "cp docker-compose.sd-launch.yml ${env.DEVPROJCOMPOSEDIR}"
    // sh "cp docker-compose.sd-label.yml ${env.DEVPROJCOMPOSEDIR}"
    
    stage "Build Application"
    dir("${env.DEVPROJCOMPOSEDIR}") {
        sh "docker-compose build"
        // sh "docker-compose push" <-- either to hub.docker.com or our own registry
        // sh "docker-compose bundle -o <bundle -- name>"
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
        // sh "docker-compose -p serv -f docker-compose.sd-launch.yml up -d"
        // sh "docker-compose -f docker-compose.yml -f docker-compose.sd-label.yml up -d"
        sh "echo this is Just a demo because it a long week"
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
