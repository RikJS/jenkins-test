node {
    stage('Artifactory') {
        def server = Artifactory.server 'artifactory1'

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

         server.publishBuildInfo buildInfo1
    }
    stage('SonarQube analysis') {
            // requires SonarQube Scanner 2.8+
            def scannerHome = tool 'SonarQube Scanner 2.8';
            withSonarQubeEnv('sonar1') {
              sh "${scannerHome}/bin/sonar-scanner " +
               "-Dsonar.projectKey=jenkinstest:project " +
               "-Dsonar.sources=src "
            }
    }
}