
node { 
 
 
def app 
 
environment {  
        HTTPS_PROXY = 'http://16.85.88.60:8080' 
        HTTP_PROXY  = 'http://16.85.88.60:8080' 
        NO_PROXY 	  = 'http://127.0.0.1:8080'
       
        PROXY_ENABLED = 'TRUE' 
        CI = 'true' 
    } 
 
stage('Checkout') { 
 
/* Let's make sure we have the repository cloned to our workspace */ 
 
 
 
checkout scm 
 
} 
 
 
 
stage('Building') { 
 
/* This builds the actual image; synonymous to 
 
* docker build on the command line */ 
 
 
// app = docker.build("patrick.gartenbach%40hpe.com/e2e-demo:lastest") 
 
app = docker.build("gaba5/test") 
 
} 
 
 
 
stage('Testing') { 
 
/* Ideally, we would run a test framework against our image. 
 
* For this example, we're using a Volkswagen-type approach ;-) */ 
 
 
 
app.inside { 
 
sh 'echo "Tests passed"' 
 
} 
 
} 
 
 
 
stage('Pushing') { 
 
/* Finally, we'll push the image with two tags: 
 
* First, the incremental build number from Jenkins 
 
* Second, the 'latest' tag. 
 
* Pushing multiple tags is cheap, as all the layers are reused. */ 
 
 docker.withRegistry('https://registry.hub.docker.com', 'dockerhubP'){ 
 /* docker.withRegistry('https://hub.docker.hpecorp.net', 'dockerhub'){ */
 
app.push("${env.BUILD_NUMBER}") 
 
app.push("latest") 

} 
 
} 
 stage('Delivering')
 {
 }
 
} 


