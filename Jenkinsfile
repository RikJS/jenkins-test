node {
def server = Artifactory.server 'art-1'

def uploadSpec = """{
  "files": [
    {
      "pattern": "*",
      "target": "jenkins-test/"
    }
 ]
}"""

 def buildInfo1 = server.upload spec: uploadSpec

 def downloadSpec = """{
  "files": [
   {
       "pattern": "*",
       "target": "jenkins-test/"
     }
  ]
 }"""

 def buildInfo2 = server.download spec: downloadSpec

 buildInfo1.append buildInfo2

 server.publishBuildInfo buildInfo1
}