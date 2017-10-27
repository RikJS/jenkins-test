node {
def server = Artifactory.newServer url: 'http://192.168.99.100:32770/artifactory/', username: 'admin', password: 'password'

def uploadSpec = """{
  "files": [
    {
      "pattern": "jenkins-test/*",
      "target": "jenkins-test/"
    }
 ]
}"""

 def buildInfo1 = server.upload spec: uploadSpec

 def downloadSpec = """{
  "files": [
   {
       "pattern": "jenkins-test/*",
       "target": "jenkins-test/"
     }
  ]
 }"""

 def buildInfo2 = server.download spec: downloadSpec

 buildInfo1.append buildInfo2

 stage('Artifactory') {
      server.publishBuildInfo buildInfo1
 }

 stage('SonarQube analysis') {
     // requires SonarQube Scanner 2.8+
     def scannerHome = tool 'SonarQube Scanner 2.8';
     withSonarQubeEnv('sonar-1') {
       sh "${scannerHome}/bin/sonar-scanner"
     }
}