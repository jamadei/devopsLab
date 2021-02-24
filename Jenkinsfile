pipeline {
    agent any

    tools {
        maven 'M3'
    }

    stages {
        stage('Build') {
			steps {
				mvn 'package'
			}
		}
        
        stage('Test with snyk') {
             steps {
               snykSecurity snykInstallation: 'Snyk1', snykTokenId: 'Snyk_token' 
              }
        }
        
    }

}
def mvn(def args) {
    def mvnHome = tool 'M3'
    def javaHome = tool 'JDK11'

    // Apache Maven related side notes:
    // --batch-mode : recommended in CI to inform maven to not run in interactive mode (less logs)
    // -V : strongly recommended in CI, will display the JDK and Maven versions in use.
    //      Very useful to be quickly sure the selected versions were the ones you think.
    // -U : force maven to update snapshots each time (default : once an hour, makes no sense in CI).
    // -Dsurefire.useFile=false : useful in CI. Displays test errors in the logs directly (instead of
    //                            having to crawl the workspace files to see the cause).

    // Advice: don't define M2_HOME in general. Maven will autodetect its root fine.
    // See also
    // https://github.com/jenkinsci/pipeline-examples/blob/master/pipeline-examples/maven-and-jdk-specific-version/mavenAndJdkSpecificVersion.groovy
    sh "${mvnHome}/bin/mvn ${args} --batch-mode -V -U -e -Dsurefire.useFile=false"
   
}

