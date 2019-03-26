node{
   stage('SCM Checkout'){
     git 'https://github.com/rsxyz/hello-jenkins'
   }
   stage('Compile-Package'){
      // Get maven home path
      def mvnHome =  tool name: 'localMaven', type: 'maven'   
      sh "${mvnHome}/bin/mvn package"
   }
 // stage('SonarQube Analysis') {
  //      def mvnHome =  tool name: 'localMaven', type: 'maven'
  //      withSonarQubeEnv('sonar') {
//          sh "${mvnHome}/bin/mvn sonar:sonar"
//        }
//    }

        stage('Artifactory Deploy') {
            def server = Artifactory.server "local-artifactory"
            def buildInfo = Artifactory.newBuildInfo()
            def rtMaven = Artifactory.newMavenBuild()
            rtMaven.tool = 'localMaven'
            rtMaven.deployer releaseRepo:'libs-release-local', snapshotRepo:'libs-snapshot-local', server: server
            rtMaven.resolver releaseRepo:'libs-release', snapshotRepo:'libs-snapshot', server: server
            rtMaven.run pom: 'pom.xml', goals: 'clean install -Dmaven.test.skip=true', buildInfo: buildInfo
            publishBuildInfo server: server, buildInfo: buildInfo
        }

}


