node {
    def app
    when {
    branch 'devOps'
    }
    stage('Clone repository') {
        checkout scm
    }
    stage('Build image') {
       app = docker.build("katerinapoposka/kiii_jenkins")
    }
    stage('Push image') {   
        docker.withRegistry('https://registry.hub.docker.com', 'dockerhub') {
            app.push("${env.BRANCH_NAME}-${env.BUILD_NUMBER}")
            app.push("${env.BRANCH_NAME}-latest")
            // signal the orchestrator that there is a new version
        }
    }
}
