node{
   stage('SCM Checkout'){
     git 'https://github.com/rsxyz/hello-jenkins'
   }
   stage('Compile-Package'){
      // Get maven home path
      def mvnHome =  tool name: 'maven-3', type: 'maven'   
      sh "${mvnHome}/bin/mvn package"
   }
}


