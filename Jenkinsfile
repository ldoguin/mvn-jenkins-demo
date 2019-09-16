node {
    def server
    def buildInfo
    def rtGradle
    
    stage ('Build') {
        git url: 'https://github.com/CleverCloud/demo-spring-boot-kotlin-statsd.git'
    }
 
    stage ('Artifactory configuration') {
        server = Artifactory.server "sprint0-artifactory"
        rtMaven = Artifactory.newMavenBuild()
        rtMaven.tool = "mvn" // Tool name from Jenkins configuration
        rtMaven.deployer releaseRepo: 'libs-release-local', snapshotRepo: 'libs-snapshot-local', server: server
        rtMaven.resolver releaseRepo: 'libs-release', snapshotRepo: 'libs-snapshot', server: server
        buildInfo = Artifactory.newBuildInfo()
    }
 
    stage ('build') {
        rtMaven.run pom: 'mvn-jenkins-demo/pom.xml', goals: 'clean install', buildInfo: buildInfo
    }
 
    stage ('Publish build info') {
        server.publishBuildInfo buildInfo
    }

}



