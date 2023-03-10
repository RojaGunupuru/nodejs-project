def registry = 'https://rojajfrog.jfrog.io'
def imageName = 'rojajfrog.jfrog.io/twittertrend-docker-local/demo-nodejsr'
def version   = '1.0.0'
pipeline{
   agent {
      node {
            label "slavegroup"
      }
   }
   tools {nodejs 'node-js'}

   stages {
      stage('build') {
            steps{
               echo "------------ build started ---------"
                  sh "npm install"
               echo "------------ build completed ---------"
      }
      }

      stage('Unit Test') {
            steps {
               echo '<--------------- Unit Testing started  --------------->'
               sh 'npm test'
               echo '<------------- Unit Testing stopped  --------------->'
            }
      }

stage(" Docker Build ") {
      steps {
      script {
         echo '<--------------- Docker Build Started --------------->'
         app = docker.build(imageName+":"+version)
         echo '<--------------- Docker Build Ends --------------->'
      }
      }
   }

   stage (" Docker Publish "){
      steps {
            script {
               echo '<--------------- Docker Publish Started --------------->'  
               docker.withRegistry(registry, 'test'){
                  app.push()
               }    
               echo '<--------------- Docker Publish Ended --------------->'  
            }
      }
   }  
  }
}
