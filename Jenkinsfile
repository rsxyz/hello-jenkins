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
	
	stage ('Artifactory Deploy'){
		def server = Artifactory.server local-artifactory
		def rtMaven = Artifactory.newMavenBuild()
		rtMaven.resolver server: server, releaseRepo: 'libs-release', snapshotRepo: 'libs-snapshot'
		rtMaven.deployer server: server, releaseRepo: 'libs-release-local', snapshotRepo: 'libs-snapshot-local'
		rtMaven.tool = 'localMaven'
                rtMaven.deployer.deployArtifacts = false // Disable artifacts deployment during Maven run
                buildInfo = Artifactory.newBuildInfo()
                rtMaven.run pom: 'pom.xml', goals: 'install', buildInfo: buildInfo
                rtMaven.deployer.deployArtifacts buildInfo
		server.publishBuildInfo buildInfo
	}
}


