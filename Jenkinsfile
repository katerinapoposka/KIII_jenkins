node {
    def app
    stage('Clone repository') {
        checkout scm
    }
    stage('Build image and push image') {
       when {
           branch 'dev'
       }
       steps {
            app = docker.build("katerinapoposka/kiii_jenkins")
            docker.withRegistry('https://registry.hub.docker.com', 'dockerhub') {
            app.push("${env.BRANCH_NAME}-${env.BUILD_NUMBER}")
            app.push("${env.BRANCH_NAME}-latest")
            // signal the orchestrator that there is a new version
       }
    }
}
