node{
   stage('SCM Checkout'){
     git 'https://github.com/rsxyz/hello-jenkins'
   }
   stage('Compile-Package'){
      // Get maven home path
      def mvnHome =  tool name: 'localMaven', type: 'maven'   
      sh "${mvnHome}/bin/mvn package"
   }
  stage('SonarQube Analysis') {
        def mvnHome =  tool name: 'localMaven', type: 'maven'
        withSonarQubeEnv('sonar') {
          sh "${mvnHome}/bin/mvn sonar:sonar"
        }
    }
}


