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
    steps {
      docker.build("trungung/docker-jenkins-pipeline:${env.BUILD_NUMBER}")
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
