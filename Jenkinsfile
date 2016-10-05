node ('swarm') {
    stage "Checkout Deployment Architecture and Operations Source"
    checkout scm
    // sh "git submodule update --init"
    
    stage "Checkout Developer Source Code"
    dir("${env.DEVPROJROOTDIR}") {
        git url: "${env.DEVPROJROOTURL}"
        sh "git submodule update --init"
        // sh "git clone --recursive ${env.DEVPROJROOTURL}"
    }
    
    stage "Build Docker Images"
    dir("${env.DEVPROJCOMPOSEDIR}") {
        sh "docker-compose build" // build --pull is failing on some nodes
    }
    
    stage "Upload Docker Images to register"
    dir("${env.DEVPROJCOMPOSEDIR}") {
        sh "docker login -u ${env.DOCKER_HUB_USER} -p ${env.DOCKER_HUB_PASSWORD}"
        sh "docker-compose push"
        sh "docker-compose pull"
    }
    
    stage "Create Application Bundle"
    dir("${env.DEVPROJCOMPOSEDIR}") {
        sh "docker-compose bundle -o polyglot.dab"
    }

    stage "Deploy Birthday App"
    dir("${env.DEVPROJCOMPOSEDIR}") {
        sh "docker stack deploy polyglot" // deploy create as well as update stack
    }
    
    stage "Configure Birthday App"
    dir("${env.DEVPROJCOMPOSEDIR}") {
        sh "docker service  update --publish-add 7979:5000 polyglot_apigateway"
    }
    
    stage "Publish Birthday App details"
    dir("${env.DEVPROJCOMPOSEDIR}") {
        sh "docker service ls"
    }
}
