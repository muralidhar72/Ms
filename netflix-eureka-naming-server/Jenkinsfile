pipeline {
	agent any
    environment {
     name='Hello'
    }
    stages {
            stage('Check env') {
              steps {
                sh "mvn -v"
                sh "java -version"
                sh "javac -version"
                sh "whoami"
                sh "printenv"
              }
            }
            // Edit the POM file for the application, setting the version to the small commit hash
            stage('Update version string in POM file') {
                steps {
                    script {
                        def pomFileName = pwd() + "/pom.xml"
                        def version = env.SMALL_HASH
                        def pomContent = readFile (pomFileName)

                        print "** current dir: " + pwd() + " **"
                        print "** version is: " + version + " **"

                        pomContent = pomContent.replace('xxxxxxxx',version)
                        writeFile file: pomFileName, text: pomContent, encoding: "UTF-8"
                        print "** written pom file **"
                    }
                }
            }
            stage('Compile, test, package and push to registry') {
              steps {
                bat "mvn clean install"
              }
            }
            // Just double check the small git hash is still there
            stage('Echo GIT commit version') {
                steps {
                    bat "echo shell env = $SMALL_HASH"
                }
            }

        }
}