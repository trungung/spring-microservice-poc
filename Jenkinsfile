node {

  def mvnHome
  stage('Preparation') { // for display purposes
    // Get some code from a GitHub repository
    git 'https://github.com/trungung/spring-microservice-poc.git'
    // Get the Maven tool.
    // ** NOTE: This 'maven' Maven tool must be configured
    // **       in the global configuration.           
    mvnHome = tool 'maven'
  }
  stage('Build') { 
    // Run the maven build
    if (isUnix()) {
      sh "'${mvnHome}/bin/mvn' -Dmaven.test.failure.ignore clean package"
    } else {
      bat(/"${mvnHome}\bin\mvn" -Dmaven.test.failure.ignore clean package/)
    }
  }
  stage('Build Docker Image') {
    dir ('sample-ping') {
      def app = docker.build "localhost:5000/sample-ping:${env.version}"
      app.push()
    }
  }
  stage('Test'){
    steps {
      sh  'echo  "TEST STAGE"' 
    }
  }
  stage('Deploy'){
    steps {
      sh  'echo  "DEPLOY STAGE"' 
    }
  }
}