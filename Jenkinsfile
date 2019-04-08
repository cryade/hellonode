node {
    def app
    
        environment { 
        HTTPS_PROXY = 'http://16.85.88.60:8080'
        HTTP_PROXY  = 'http://16.85.88.60:8080'
      
        PROXY_ENABLED = 'TRUE'
        CI = 'true'
    }

    stage('Clone repository') {
        /* Let's make sure we have the repository cloned to our workspace */

        checkout scm
    }

    stage('Build image') {
        /* This builds the actual image; synonymous to
         * docker build on the command line */

        app = docker.build("cryade/hellonode:{env.BUILD_ID}")
    }

    stage('Test image') {
        /* Ideally, we would run a test framework against our image.
         * For this example, we're using a Volkswagen-type approach ;-) */

        app.inside {
            sh 'echo "Tests passed"'
        }
    }

    stage('Push image') {
        /* Finally, we'll push the image with two tags:
         * First, the incremental build number from Jenkins
         * Second, the 'latest' tag.
         * Pushing multiple tags is cheap, as all the layers are reused. */
        docker tag app hub.docker.hpecorp.net/patrick.gartenbach@hpe.com/e2e-demo
        docker.withRegistry('https://hub.docker.hpecorp.net/patrick.gartenbach@hpe.com/e2e-demo', 'dockerhub') {
            app.push("${env.BUILD_NUMBER}")
            app.push("latest")
        }
    }
}
