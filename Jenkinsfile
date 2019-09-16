node {
    def server
    def buildInfo
    def rtGradle
    
    stage ('Build') {
        git url: 'https://github.com/ldoguin/mvn-jenkins-demo.git'
    }
 
    stage ('Artifactory configuration') {
        server = Artifactory.server "sprint0-artifactory"
        rtMaven = Artifactory.newMavenBuild()
        rtMaven.tool = "mvn" // Tool name from Jenkins configuration
        rtMaven.deployer releaseRepo: 'libs-release-local', snapshotRepo: 'libs-snapshot-local', server: server
        buildInfo = Artifactory.newBuildInfo()
    }
 
    stage ('build') {
        rtMaven.run pom: 'pom.xml', goals: 'clean install', buildInfo: buildInfo
    }
 
    stage ('Publish build info') {
        server.publishBuildInfo buildInfo
    }

}



